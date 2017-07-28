title: ionic不同view跳转到同一个view并保留历史的路由设计
date: 2016-11-29 07:08:08
updated: 2016-11-30 01:08:08
tags:
	- Ionic
---


最近手上的 ionic 项目，从左边侧滑的交互方式换到了 tabs 的交互方式。
以前的树形路由需要改造成网状的。
于是开始在网上搜索有没有现成的技术方案，找了一圈下来发现，ionic 的社区里都是一些没法解决的回复。
但是自己翻看 ui-router 的时候发现 guide 里面是有网状路由设计的。
看逻辑图

   
  <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/ionic-different-view-jump-to-the-same-view-and-keep-history-of-routing-design.png">
       <img alt="路由图" src="http://resource.zwjay.cn/jekyll/img/ionic-different-view-jump-to-the-same-view-and-keep-history-of-routing-design.png" />
  </a>


上代码：state 里面新加一个状态

```javascript
.state("other", {
    url: "/other",
    abstract: true,
    controller: "OtherCtrl",
    template: "<ion-nav-view></ion-nav-view>",
    onEnter: function($rootScope, fromStateServ) {
        fromStateServ.setState("other", $rootScope.fromState, $rootScope.fromParams);
    }
})
```

对应的controller

```javascript
.controller("OtherCtrl", function($scope, $state, fromStateServ) {
    $scope.backNav = function() {
        var fromState = fromStateServ.getState("other");
        if (fromState.fromState !== undefined) {
            $state.go(fromState.fromState.name, fromState.fromParams);
        } else {
            //设置没有历史的时候，默认的跳转
            $state.go("app.xxx");
        }
    };
})
```

保留 history 的公共方法

```javascript
.factory("fromStateServ", function() {
    return {
        data: {},
        setState: function(module, fromState, fromParams) {
            this.data[module] = {
                "fromState": fromState,
                "fromParams": fromParams
            };
        },
        getState: function(module) {
            return this.data[module];
        }
    };
})
```
