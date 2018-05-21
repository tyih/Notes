## 1.指针运算
在内存中取出数据

```
x8 = sp + 0x4 地址 4个字节区域 *a
w9 = 10 值 立即数给了w9寄存器 b = 10
[sp + 0x4] = w9 值 写入sp + 0x4寄存器区域 x8 = &w9
[sp + 0x8] = x8 值 把x8地址值放入栈中 x8寄存器值放入栈中
```

静态分析：汇编代码，分析App源码
动态调试：界面调试，Cycript\Xcode LLDB
代码注入：动态库，hook代码，改变原来程序执行流程
重签名：安装非越狱手机上

## class-dump
导出头文件：class-dump -H WeChat -o WechatH

## MachO文件（Mach Object）
总共有11种格式，是Mac\iOS上存储程序、库的标准格式
1.可执行文件
2.object (clang -c xx.c   /  file xxx.o  /  clang xx.o  /  clang -o yyy text.o  /  clang -o demo test1.c text.c)
 - .o文件 
 - .a静态库文件，N个.o文件
3.DYLIB：动态库文件
 - .dylib (Mac)
 - .framework (iOS)
4.动态连接器
5.DSYM

## 动态库 共享缓存 (/private/var/db/dyld/)
为了提高性能，系统的动态库文件都存到了动态库共享缓存里面

## 动态加载器 dyld (/usr/lib/) 调用动态库
dynamic loader \ Mach-O 64-bit dynamic linker