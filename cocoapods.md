
## cocoapods 

1.pod install
	如果podfile.lock存在，则直接从此文件中读取框架信息，下载安装
	如果不存在，会读取podfile文件内的框架信息，下载好后根据下载好的框架信息，生成podfile.lock文件

2.pod update
不管podfile.lock是否存在，都会读取podfile文件的框架信息去下载，下载好后根据下载好的框架信息，生成podfile.lock文件

podfile文件内框架信息，没有指定具体的版本
开发中一般选择pod install而不是pod update，为了开发中大家使用的第三方版本一致

## 远程索引库
所有的框架描述信息都存在里面，.spec文件（框架的名称、版本号、远程地址...）

pod setup，把远程索引库克隆下来，生成一个本地索引库 ~/.cocoapods/repos/master/Specs/
pod search，从本地索引库里检索框架描述信息文件，但描述文件过多，不可能每个文件对比，第一次pod search时会下载一个检索的索引文件 /Users/igen-tech/Library/Caches/CocoaPods/search_index.json
pod install，根据检索到的框架信息找到真正存放代码的远程地址，再把它下载集成到工程中

## 创建cocoapod仓库
	1.本地代码仓库与远程仓库链接
		git init
		git remote add origin https://github.com/xxx
	2.创建.spec文件
		pod spec create xxx
		git tag '0.0.1'
		git push --tags
	  s.source_files：过滤我们从仓库中需要下载的文件
	3.上传.spec文件到远程索引库
		注册一下trunk：pod trunk register 邮箱 '作者' --verbose
		上传.spec文件到远程索引库：pod trunk push
	4.更新本地索引库，并把索引索引文件删掉
		pod setup
		pod search