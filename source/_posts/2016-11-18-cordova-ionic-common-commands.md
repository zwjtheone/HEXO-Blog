title: cordova ionic 常用命令
date: 2016-11-18 20:08:08
updated: 2016-11-30 20:08:08
tags:
	- Cordova
	- Ionic
---

# 安装 cordova：

npm install -g cordova

# 创建应用程序

cordova create hello com.example.hello HelloWorld 

# 添加平台

cordova platform add android

cordova platform add ios

<!--more-->

# 完成后运行以下命令查看：

cordova platfrom list

# 移除Android平台支持

cordova platform rm android

# 运行以下命令编译应用程序：

cordova build

或

cordova build android  //只针对Andorid平台编译

实际上build命令相当于以下两个命令，只不过cordova prepare 不执行编译,只是把你修改的程序复制到可以编译的目录下面：

cordova prepare android  

cordova compile android

# 启动模拟器：

cordova emulate android

# 添加插件：

可以用CLI搜索可用的插件：

cordova plugin search bar code

# 安装插件

比如:

cordova plugin add org.apache.cordova.device                   //设备API

cordova plugin add org.apache.cordova.network-information  //网络（事件）

cordova plugin add org.apache.cordova.battery-status      //电池（事件）

cordova plugin add org.apache.cordova.device-motion     //加速器

cordova plugin add org.apache.cordova.device-orientation     //罗盘

cordova plugin add org.apache.cordova.geolocation         //定位

cordova plugin add org.apache.cordova.camera                 //摄像头

cordova plugin add org.apache.cordova.media-capture     //媒体文件处理

cordova plugin add org.apache.cordova.media                   //媒体文件处理

cordova plugin add org.apache.cordova.file                        //文件访问

cordova plugin add org.apache.cordova.file-transfer          //文件传输

cordova plugin add org.apache.cordova.dialogs                 //对话框

cordova plugin add org.apache.cordova.vibration              //震动

cordova plugin add org.apache.cordova.contacts               //联系人

cordova plugin add org.apache.cordova.globalization       //全球化

cordova plugin add org.apache.cordova.splashscreen       //闪屏

cordova plugin add org.apache.cordova.inappbrowser             //打开新的浏览器窗口

cordova plugin add org.apache.cordova.console                //调试控制台

# 你可以用以下命令查看所有已经安装的插件

cordova plugin ls

# 使用以下命令删除插件：

cordova plugin rm org.apache.cordova.console    

# 或者通过地址来添加插件：

cordova plugin add https://github.com/apache/cordova-plugin-console.git

# 帮助：

cordova help

# 更新cordova：

npm update -g cordova

# cordova更新完成后，还需要更新项目：

cordova platform update android

# 编译发行版
$ ionic build android --release
# 生成签名
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
# 签名，注意目录需一致
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore android-release-unsigned.apk myApp-alias
# zipalign
D:android\build-tools\22.0.1\zipalign -v 4 android-release-unsigned.apk E:\myApp.apk

可以把 `android\build-tools\22.0.1\` 加入环境变量 `PATH` 
