title: ionic应用中的文字不能长按复制、粘贴问题解决
date: 2016-11-30 10:01:08
update: 2016-11-30 10:08:08
tags:
	- Ionic
---

直接上代码：

# >html部分

```html
<html ng-app="ionicApp">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
    <title>Ionic文字复制问题</title>
    <link href="http://code.ionicframework.com/1.0.0-beta.4/css/ionic.css" rel="stylesheet">
    <script src="http://code.ionicframework.com/1.0.0-beta.4/js/ionic.bundle.js"></script>
</head>
<body ng-controller="MyCtrl">
    <ion-header-bar class="bar-positive">
        <h1 class="title">ionic 测试copy</h1>
    </ion-header-bar>
    <ion-content overflow-scroll='true'>
        <div class="selectable">幻灯片1测试文字，试试可以复制</div>
    </ion-content>
</body>
</html>
```


# >css部分

```css
ion-content{
  overflow-scroll: true;
}
.scroll-content {
  -webkit-user-select: auto !important;
  -moz-user-select: auto !important;
  -ms-user-select: auto !important;
  user-select: auto !important;
}

.selectable {
  -webkit-user-select: auto;//控制网页内容选择范围
}
```

# >js部分

```javascript
angular.module('ionicApp', ['ionic'])
.controller('MyCtrl', function($scope) {
  stop_browser_behavior: false  
self.touchStart = function(e) {
  self.startCoordinates = getPointerCoordinates(e);
  if ( ionic.tap.ignoreScrollStart(e) ) {
    return;
  }
  if( ionic.tap.containsOrIsTextInput(e.target) ) {
    // do not start if the target is a text input
    // if there is a touchmove on this input, then we can start the scroll
    self.__hasStarted = false;
    return;
  }
  self.__isSelectable = true;
  self.__enableScrollY = true;
  self.__hasStarted = true;
  self.doTouchStart(e.touches, e.timeStamp);
  // e.preventDefault();
};
});

```

通过代码我们可以看到，首先在html中,添加overflow-scroll='true'，然后在我们想要复制文字的容器上，添加自定义类，代码中我们添加的是'.selectable' ，在这个类上设置我们的css样式。

>这里需要注意的是，这个自定义类，不能加在ionic的特定标签上。如下：

```html
<ion-content class="selectable" overflow-scroll="true">
```

这样写，是无效的，我们必须这样写：

```html
<ion-content overflow-scroll='true'> 
     <div class="selectable">幻灯片1测试文字，试试可以复制</div> 
</ion-content>
```

表示我就是因为这个没写对，调试了半天出不来效果。。。

最后一步就是在页面对应的controller里面拷贝如上js代码。
