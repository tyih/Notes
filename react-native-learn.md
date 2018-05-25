
## 搭建react-native环境

### 1.安装Homebrew https://brew.sh/index_zh-cn.html

### 2.安装Node.js
$brew install node
> npm: Node.js的模块依赖管理工具。React Native源代码以及开发React Native应用用到的第三方组件都可以通过npm进行下载安装。
> 注意⚠️: 因为要从npm下载React Native的源代码，可能需要等待一会。如果长时间没有反应，建议翻墙。也可以将npm替换为国内镜像：
$npm config set registry https://registry.npm.taobao.org --global
$npm config set disturl https://npm.taobao.org/dist --global

### 3.安装watchman(Facebook用于监视JavaScript文件改动的开源项目)
$brew install watchman

### 4.安装flow(Facebook开源的一个JavaScript静态类型检查器，用于发现JavaScript程序中的类型错误)
$brew install flow

### 5.安装react-native-cli(react-native-cli是React Native的命令行工具，安装react-native-cli后我们就能够通过react-native相关命令管理ReactNative工程)
$npm install -g react-native-cli

-------------------------------------------------------------------

## 开发工具

### Deco IDE
一款专门用于开发React Native应用的IDE

### 使用VSCode

--------------------------------------------------------------------

## Tips
* 将jsbundle重新打包
$react-native bundle --entry-file App.js --platform ios --dev false --bundle-output ./release/main.jsbundle --assets-dest ./release

* find out which process
$lsof -n -i4TCP:8081

* shut down the other process
$kill -9 <PID> 

---------------------------------------------------------------------

### rn增量升级方案
http://bbs.reactnative.cn/topic/276/reactnative%E5%A2%9E%E9%87%8F%E5%8D%87%E7%BA%A7%E6%96%B9%E6%A1%88

### 开发工具
https://www.cnblogs.com/vipstone/p/7125338.html