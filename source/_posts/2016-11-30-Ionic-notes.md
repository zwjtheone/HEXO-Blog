title: Ionic 笔记
date: 2016-11-30 07:08:08
updated: 2016-11-30 01:08:08
tags:
	- Ionic
---

# ion-content的回弹效果没有了

- 在 `<ion-content>` 标签加上 `overflow-scroll="false" has-bouncing="true"

# view之间的数据传输

## 1 .使用 `$state.go(to [, toParams] [, options])`
在第二个参数传入一个JSON对象，在 `to` 的路由加上params:{} 定义传输的参数,然后在 `to` 的 `controller` 注入 `$stateParams` 接收数据。

<!--more-->

``` javascript
$state.go("tab.lazy", {lazyId:1, lazyName:2}, {inherit:false});

-------------------------------------------------------------------

.state('tab.lazy', {
        url: '/lazy',
        views: {
          'tab-lazy': {
            templateUrl: 'templates/lazy.html',
            controller: 'LazyCtrl'
          }
        },
        params: {
          lazyId: null,
          lazyName: null
        }
})
      
-------------------------------------------------------------------

.controller('venueDetailsCtrl', function ($scope, $stateParams, $http) {
    $scope.lazyId = $stateParams.lazyId
    $scope.lazyName = $stateParams.lazyName
})
```

**第三个配置参数： Object**
* `location` *Boolean or "replace" (default true)*, If `true` will update the url in the location bar, if `false` will not. If string `"replace"`, will update url and also replace last history record.
* `inherit` *Boolean (default true)*, If `true` will inherit url parameters from current url.
* `relative` *stateObject (default $state.$current)*, When transitioning with relative path (e.g '^'), defines which state to be relative from.
* `notify` *Boolean (default true)*, If `true` will broadcast $stateChangeStart and $stateChangeSuccess events.
* `reload` `v0.2.5` *Boolean (default false)*, If `true` will force transition even if the state or params have not changed, aka a reload of the same state. It differs from reloadOnSearch because you'd use this when you want to force a reload when *everything* is the same, including search params.

- 如果`$state.go` 跳转没有动画效果，可以加上
```javascript
$ionicViewSwitcher.nextDirection('forward'); // 'forward', 'back'
```

## 2 .利用ui-serf 

在`ui-serf='lazy'` 后面加上参数-> `ui-serf='lazy({lazyId: 1,lazyName: 2})'` ,一样在路由上加params,用$stateParams接收。

## 3 .利用url（a 标签）
```javascript
$stateProvider
    .state('contacts.detail', {
        url: "/contacts/:contactId",
        templateUrl: 'contacts.detail.html',
        controller: function ($stateParams) {
            // If we got here from a url of /contacts/42
            expect($stateParams).toBe({contactId: "42"});
        }
    })
```

主要在 `:contactId` ,注意前面要加上`/`,当然也可以用花括号,`url: "/contacts/{contactId}" `,
- '/hello/' - Matches only if the path is exactly '/hello/'. There is no special treatment for trailing slashes, and patterns have to match the entire path, not just a prefix.
- '/user/:id' - Matches '/user/bob' or '/user/1234!!!' or even '/user/' but not '/user' or '/user/bob/details'. The second path segment will be captured as the parameter 'id'.
- '/user/{id}' - Same as the previous example, but using curly brace syntax.
- '/user/{id:int}' - The param is interpreted as Integer.

**用法**

```html
<a ui-sref="contacts.detail({contactId: id})">View Contact</a>
```

# 数据更新,页面没有更新

## $apply  方法 作用：

Scope 提供$apply 方法传播 Model 的变化

### $apply  方法 使用情景 ：

AngularJS 外部的控制器（DOM 事件、外部的回调函数如 jQuery UI 空间等）调用了 AngularJS 函数之
后，必须调用$apply。在这种情况下，你需要命令 AngularJS 刷新自已（模型、视图等） ，$apply 就是
用来做这件事情的。

```javascript
xxx
$scope.apply();
___
$scope.apply(function() {
  xxx
})
```

### $apply  方法 注意事项 ：

只要可以， 请把要执行的代码和函数传递给$apply 去执行， 而不要自已执行那些函数然后再调用$apply。

# 跳转过渡动画

## $state.go
```javascript
$state.go('myState',{
    navTransition:'android',
'navDirection':'forward'
});
```
 
## ui-sref
```html
<div ui-sref='myState' nav-direction="forward" nav-transition='android'>Some element</div>
```

## $ionicViewSwitcher
```javascript
$ionicViewSwitcher.nextDirection('forward');// 'forward', 'back', etc.
$state.go('myState');
```

# Angular 获取事件焦点或其他信息 （ng-click on-tap 等事件）

```html
<a href="#" ng-click="brandFnc($event)">brList</a>
```

```javascript
$scope.brandFnc = function($event){
    // 通过 $event.target 来获取
}
```

# ionic actionsheet 安卓样式问题

如果想统一为ios的样式，打开ionic css文件，找到这一段 注释掉。

```css

.platform-android .action-sheet-backdrop.active {
background-color: rgba(0, 0, 0, 0.2);
}

.platform-android .action-sheet {
margin: 0;
}

.platform-android .action-sheet .action-sheet-title,
.platform-android .action-sheet .button {
text-align: left;
border-color: transparent;
font-size: 16px;
color: inherit;
}

.platform-android .action-sheet .action-sheet-title {
font-size: 14px;
padding: 16px;
color: #666;
}

.platform-android .action-sheet .button.active,
.platform-android .action-sheet .button.activated {
background: #e8e8e8;
}

.platform-android .action-sheet-group {
margin: 0;
border-radius: 0;
background-color: #fafafa;
}

.platform-android .action-sheet-cancel {
display: none;
}

.platform-android .action-sheet-has-icons .button {
padding-left: 56px;
}

```

# angular 选中当前节点
```javascript
$scope.brandFnc = function($event){
    $event.currentTarget
}
```

# ionic中使用 iframe 可能遇到的问题

## 无法访问外部url的问题--两个步骤解决：
1.iframe的src属性用ng-src属性替代，并指明绑定对象： ng-src="{{targetUrl}}"
2.在controller里，调用$sce: $scope.targetUrl = $sce.trustAsResourceUrl(url)
## 高度无法最大化的问题--两个步骤解决：
1.ion-content 属性里添加  scroll="true" overflow-scroll="true"，[参考](https://github.com/driftyco/ionic/issues/1151)  
2.iframe的style里添加 min-height: 100%，[参考](https://forum.ionicframework.com/t/fill-content-container/605)

# Angular 上传中 file change ng-change无效的解决方法


```html
<div ng-controller="form-cntlr">
    <form>
         <button ng-click="selectFile()">Upload Your File</button>
         <input type="file" style="display:none" id="file" name='file' 
         onchange="angular.element(this).scope().fileNameChanged(this)" />
    </form>  
</div>
```

[ng-file-upload](https://github.com/danialfarid/ng-file-upload)
[ngUpload - An AngularJS Service for uploading files using iframe](http://ngmodules.org/modules/ngUpload)

# ionic打包 resource报错 

> ionic 文件夹中的文件不能带有中文。


# ionic 锚点跳转

[https://forum.ionicframework.com/t/anchor-scroll-flash/4390/9](https://forum.ionicframework.com/t/anchor-scroll-flash/4390/9)

```javascript
$scope.scrollNextActivity = function(index){ 
    $location.hash(index); 
    $ionicScrollDelegate.anchorScroll(true); 
};
```

进入页面时或者触发某操作时调用 scrollNextActivity('id') 即可

# ionic获取距离顶部的距离

> getScrollPosition()
>> Returns: `object` The scroll position of this view, with the following properties:
>> `{number}` `left` The distance the user has scrolled from the left (starts at 0).
>> `{number}` `top` The distance the user has scrolled from the top (starts at 0).
>> `{number}` `zoom` The current zoom level.

```javascript
$ionicScrollDelegate.getScrollPosition().top 
```

# ionic 判断滚动到页面底部

```html
<ion-scroll delegate-handle="scroller" direction="y" style="width: 100%; height: 100%">
    <p> Your Ionic App Scrollable Content Here </p>
</ion-scroll>
```

```javascript
$scope.checkScroll = function () {
    var currentTop = $ionicScrollDelegate.$getByHandle('scroller').getScrollPosition().top;
    var maxScrollableDistanceFromTop = $ionicScrollDelegate.$getByHandle('scroller').getScrollView().__maxScrollTop;
    
    if (currentTop >= maxScrollableDistanceFromTop)
    {
      $scope.toggleTopMenu();
    }
};
```


# ionic input 点击时 弹出键盘挡住input输入框

[http://www.ionic.wang/js_doc-index-id-66.html](http://www.ionic.wang/js_doc-index-id-66.html)

使用该插件的用法可以参考 [https://github.com/driftyco/ionic-plugins-keyboard](https://github.com/driftyco/ionic-plugins-keyboard)

[http://ionicframework.com/docs/api/directive/keyboardAttach/](http://ionicframework.com/docs/api/directive/keyboardAttach/)

# ionic serve 打开时显示ios和android两个视图

```
ionic serve -l -c --browser
```

[https://github.com/leob/ionic-quickstarter](https://github.com/leob/ionic-quickstarter)

# ionic 禁止横屏
1、添加插件

> cordova plugin add net.yoik.cordova.plugins.screenorientation  

2、添加屏幕配置 (Config.xml文件里面添加)

```html
<preference name="orientation" value="portrait" />  
```

3、在Index.html 界面 添加JS 屏幕监听事件

```javascript
<script>  
    document.addEventListener("deviceready", onDeviceReady, false);  
    function onDeviceReady()  
    {  
  
       var so = cordova.plugins.screenorientation;  
       so.setOrientation(so.Orientation.LANDSCAPE);  
    }  
</script>  
```


# ionic android 按两下后退件退出APP

```javascript
var backbutton = 0;
$ionicPlatform.registerBackButtonAction(function() {
  if ($location.path() === "/home") {
    if(backbutton == 0){
      backbutton++;
      $cordovaToast.showLongBottom('Press again to exit');
      // $timeout(function(){
      //   backbutton=1;
      // },5000);
    }else{
      navigator.app.exitApp();
    }
  }else{
    $ionicHistory.goBack();
  }
}, 100);
```
# ionic tab图标自定义用png图片

```css
.tabs .tab-item .icon.my-icon-AA-on {
  background-repeat: no-repeat;
  background-position: 50%;
  background-size: 25px;
  background-image: url("../img/tabs/aa-on.png");
}

.tabs .tab-item .icon.my-icon-AA-off {
  background-repeat: no-repeat;
  background-position: 50%;
  background-size: 25px;
  background-image: url("../img/tabs/aa-off.png");
}
```
在`tab.html`中,icon-off icon-on 为自定义的类名。

```html
  <ion-tab title="AA" icon-off="my-icon-AA-off" icon-on="my-icon-AA-on" href="#/tab/aa_against">
    <ion-nav-view name="tab-aa"></ion-nav-view>
  </ion-tab>
```

# 报错events.js:72throw er; // Unhandled 'error' event

```
The error is:
=======================================
events.js:72
throw er; // Unhandled 'error' event
^
Error: spawn ENOENT
at errnoException (child_process.js:1000:11)
at Process.ChildProcess._handle.onexit (child_process.js:791:34)

```

解决的方法很简单，将ionic换成cordova即可。

```
cd myApp
cordova platform add android //这行可能会报错
cordova build android
cordova emulate android
```

# 生成项目(ionic start myApp tabs)时可能会报错

`Error: command failed:fatal:could not create work tree dir:'C:\Users/ADMINI~1\AppData\Local\Temp\plugman\git\1402853493773'.:No such file or directory`

解决办法：进入上面对应的目录，建立对应的文件。比如在temp目录下建立plugman目录，在plugman目录下建立git目录，然后再git下建立1402853493773目录。即可，经测试有效。

# node-gyp: Permission denied 安装软件包报错

这个一般是centos等系统，在root用户下安装会报错。主要是权限问题，报错详情：

```
> node-gyp rebuild

 sh: 1: node-gyp: Permission denied
 \
 > ws@0.4.32 install /root/.nvm/versions/node/v0.12.4/lib/node_modules/log.io/node_modules/socket.io-client/node_modules/ws
 > (node​​-gyp rebuild 2> builderror.log) || (exit 0)


 > ws@0.4.32 install /root/.nvm/versions/node/v0.12.4/lib/node_modules/log.io/node_modules/socket.io/node_modules/socket.io-client/node_modules/ws
 > (node​​-gyp rebuild 2> builderror.log) || (exit 0)

 npm ERR! Linux 3.13.0-48-generic
 npm ERR! argv "/root/.nvm/versions/node/v0.12.4/bin/node" "/root/.nvm/versions/node/v0.12.4/bin/npm" "install" "-g" " log.io"
 npm ERR! node v0.12.4
 npm ERR! npm v2.10.1
 npm ERR! file sh
 npm ERR! code ELIFECYCLE
 npm ERR! errno ENOENT
 npm ERR! syscall spawn

 npm ERR! contextify@0.1.14 install: `node-gyp rebuild`
 npm ERR! spawn ENOENT
 npm ERR!
 npm ERR! Failed at the contextify@0.1.14 install script 'node-gyp rebuild'.
 npm ERR! This is most likely a problem with the contextify package,
 npm ERR! not with npm itself.
 npm ERR! Tell the author that this fails on your system:
 npm ERR! node-gyp rebuild
 npm ERR! You can get their info via:
 npm ERR! npm owner ls contextify
 npm ERR! There is likely additional logging output above.

 npm ERR! Please include the following file with any support request:
 npm ERR! /root/npm-debug.log
```

可以清楚看到讯息中提示我们在执行node-gyp 的时候权限不足。查询一下Google ，找到别人blog写得简单解决方法：

```
npm config set unsafe-perm true
```

接下来安装就正常了。 至于npm config的使用方法， 请参考 [此处](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-CN&prev=search&rurl=translate.google.com.sg&sl=zh-TW&u=https://docs.npmjs.com/misc/config&usg=ALkJrhjNU7KHzjR4I6JC5IMFf4Ffcg3KaA) .
我们可以从npm config set unsafe-perm的解说中看到，我们刚刚修改的意思。

# .gitignore 默认排除了 plugins 文件夹，团队其他人 clone 了项目后缺少插件，一个一个装太麻烦

`ionic platform add/remove xxx` 以及 `ionic plugin add/remove xxx` 的时候，`Ionic CLI` 都在 `package.json` 中保存了项目的状态。clone 完后可以使用 **`ionic state restore`** 命令快速恢复
也可以在`.gitignore`中删除`plugins一行`

# 在哪里查看 Ionic 带的所有图标？

[http://ionicons.com](http://ionicons.com)

# 第一次`ionic platform add xxx` 会等很久

正常，第一次会下载gradle等打包文件，约100M左右，先睡一觉吧，建议挂上VPN，也可以百度自己手动添加gradle。

# tel:xxxxx sms:xxxxxx mailto:xxxxxx geo:xxxxxx 一类的链接不能唤起其他应用。

```html
<access origin="*"/>
<access origin="tel:*" launch-external="yes"/>
<access origin="sms:*" launch-external="yes"/>
<access origin="mailto:*" launch-external="yes"/>
<access origin="geo:*" launch-external="yes"/>

<allow-intent href="tel:*"/>
<allow-intent href="sms:*"/>
<allow-intent href="mailto:*"/>
<allow-intent href="geo:*"/>
```



# mac,chrome 对真机运行的app进行调试。

插上数据线。打开应用
mac，打开safari，Safari -> 开发 -> 手机名 -> 应用名。
chrome，地址栏输入 chrome://inspect , 点击inspect。

# ionic serve 或在实机调试时开启了 livereload 功能时的跨域问题

chrome 搜索插件，`Access-Control-Allow-Credentials` 安装打开，可以屏蔽跨域限制。

# APP开启检测网络并提示开启

1、https://github.com/apache/cordova-plugin-network-information
2、https://github.com/apache/cordova-plugin-dialogs
3、https://github.com/deefactorial/Cordova-open-native-settings

具体用法请查看文档。

# 极光推送设置分组的坑

服务器端网上代码很多，不多说了，客户端中有个坑

```javascript
window.plugins.jPushPlugin.setTagsWithAlias(tagname,alias);
```

其中 `tagname/alias` 都为 `string` , （看网上好多人这么搞的，不明白他们怎么成功的？）
返回错误 `Error reading tagAlias JSON`
再试

```javascript
window.plugins.jPushPlugin.setTagsWithAlias([tagname],alias);
```

这样OK。 换句话说， tags是`数组`， alias是`string`

# ionicLoading 以及网络超时写法

app.js中，先注册rootScope的广播

```javascript
.run(function ($ionicPlatform,$ionicLoading,ToastService, $rootScope) {
    $rootScope.$on('loading:show', function () {
        $ionicLoading.show({ template: '努力为您加载中...' })
    })
    $rootScope.$on('loading:hide', function () {
        $ionicLoading.hide()
    })

.config(function ($httpProvider) {
$httpProvider.defaults.timeout = 5000; //默认超时为5秒
$httpProvider.interceptors.push(function ($rootScope) {
        return {
            request: function (config) {
               $rootScope.$broadcast('loading:show')
                return config
            },
            response: function (response) {
               $rootScope.$broadcast('loading:hide')
                return response
            },
            responseError: function (response) {
           $rootScope.$broadcast('loading:hide')
                return response

            },
            requestError: function (config) {
                 $rootScope.$broadcast('loading:hide')
                return config
            }
        }
    })
```

# 在ion-content中，由于scorll 更新了页面数据后不能拖动到底部

由于scorll 更新了页面数据后不能拖动到底部，html页面不能完全加载，原因在于当前页面没有更新size，解决方法引入$ionicScrollDelegate；
在controller里改变高度的地方调用方法：

`$ionicScrollDelegate.resize`


# cordova插件 splashscreen 启动白屏的问题

```html
<preference name="SplashScreen" value="screen"/>
<preference name="AutoHideSplashScreen" value="false"/>
<preference name="auto-hide-splash-screen" value="false"/>
<preference name="ShowSplashScreenSpinner" value="false"/>
<preference name="SplashMaintainAspectRatio" value="true" />
<preference name="SplashShowOnlyFirstTime" value="false"/>
<preference name="SplashScreenDelay" value="10000"/>
```

取消自动隐藏（改为代码控制隐藏），把持续时间改为较大的值（10秒），设置每次打开应用都显示splash screen

P.S.默认只有SplashScreen和SplashScreenDelay，需要把其它的（SplashMaintainAspectRatio可选）都添上。

手动隐藏splash screen，在run里面添上

```javascript
.run(['$rootScope', function($rootScope) {
        // init
        // $rootScope.isLoading = false;

        // hide splash immediately
        if(navigator && navigator.splashscreen) {
            navigator.splashscreen.hide();
        }
    });
}])
```

# What went wrong:Execution failed for task ':packageRelease' > Failed to read key from keystore

解决方案：重新打包签名 android.keystore

# What went wrong:A problem occurred configuring root project 'android'.
   > Could not resolve all dependencies for configuration ':_armv7DebugCompile'.
   > Could not find any version that matches com.android.support:support-v4:[13.0.0,).
   > Searched in the following locations:
   > https://repo1.maven.org/maven2/com/android/support/support-v4/maven-metadata.xml
   > https://repo1.maven.org/maven2/com/android/support/support-v4/
   
解决方案：
打开Android SDK Manager
确保Android Suppoer Repository 和 Google Repository 已经安装
