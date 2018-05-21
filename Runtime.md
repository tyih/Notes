
## Runtime
源码 -> 编译器（静态分析） -> 中间码 -> Runtime System（对代码进行动态操作） -> 目标程序

/usr/include/objc/下的一组文件，会被Runtime System调用
与Runtime交互：
	- Objective-C Source Code 被动
	- NSObject Methods（isKindOfClass:、isMemberOfClass、respondsToSelector:、conformsToProtocol:）
	- Runtime Functions

功能：
	1.交换方法
	2.动态添加方法
	3.动态添加属性
	4.字典转模型

## 过程
	- 发送消息
		编译得到，动态绑定
		[receiver message] -> objc_msgSend(receiver, selector, arg1, arg2...) 
		Runtime数据结构
		methodLists:指向该类实例方法列表，将方法选择器和方法实现地址联系起来，可以动态修改来添加成员方法，Category实现原理（不能添加属性）
		1. Runtime把方法调用转化为消息发送，即objc_msgSend，把方法调用者，方法选择器，当参数传递过去
		2. 方法调用者通过isa指针找到所属的类，然后在cache\methodLists中查找方法，找到就跳到对应的方法(IMP)执行
		3. 如果在类中没找到方法，会检查是否有被动态加载的方法类处理该消息。如没有，则通过super_class往上查找，如果一直找到NSObject都没有找到，就放到消息转发的时候
		4. methodLists指向实例方法列表，类方法存储在元类中，Class通过isa指针可找到所属元类

	- 动态方法解析
		1. Runtime没有在本类MethodLists中找到匹配的方法，可以动态添加一个方法，进行消息转发前的第一个阶段
		2. 重载resolveInstanceMethod:和resolveClassMethod:分别实现实例方法实现和类方法实现
		   Runtime在Cache和方法分发表中提供了一次动态添加方法实现的机会，需要用到class_addMethod完成向特定类添加特定方法实现的操作

	- 消息转发
		两大阶段：
			1.先询问接收者，所属的类是否能动态添加方法--动态方法解析
			2.运行时系统请求我接收者以其他手段类处理消息
				1.查找有没有replacement receiver进行处理（forwardingTargetForSelector）
				2.把selector相关信息封装到NSInvocation对象中，如依旧未处理，则让NSObject调用doNotReconizeSelector（forwardInvocation）

## Runtime常用API
	objc_setAssociatedObject		对象关联
	objc_getAssociatedObject		对象关联
	method_exchangeImplementations	方法掉配（method swizzle）
	objc_getClassList				获取所有类的列表
	object_getIvar					读取一个实例变量的值
	class_copyPropertyList			获取属性列表（模型->字典)
	protocol_copyPropertyList		获取协议中的属性

## clang
Clang 是一个 C++ 编写、基于 LLVM、发布于 LLVM BSD 许可证下的 C/C++/Objective/Objective C++ 编译器，其目标（之一）就是超越 GCC
clang -rewrite-objc main.m

## 场景
	1.每个vc展示
		创建一个vc的分类，重写自定义ViewDidAppear，并在+load方法中实现ViewDidAppear的交换

	2.开发中需要在不改变某个类的前提下添加一个新的属性，为系统类添加新属性，可以利用Rutime的关联对象objc_setAssociatedObject

	3.字典的模型和自动转换，优秀的第三方JSONModel、YYModel等利用runtime对属性进行获取、赋值操作，比KVC转化更强大、效率

	4.JSPath替换已有的OC实现