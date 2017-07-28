title: ionic 替代 Modal 的方案
date: 2016-11-28 20:08:08
updated: 2016-11-30 20:08:08
tags:
	- Ionic
---

在 $state.go 前记录下当前的 view ，然后禁止下一个 view 记录 backView ，就不会显示后退按钮（ Android 硬件后退也不行 ）。在需要关闭时，后来加入导航栈的任意 view 中设置 backView 为记录下来的 view ，然后 back 。

<!--more-->

```javascript
// go 的时候
var backHistoryId = $ionicHistory.currentHistoryId();
var backViewId = $ionicHistory.currentView().viewId;
$ionicHistory.nextViewOptions({
  disableBack: true,
  disableAnimate: true
});
$state.go('my-awesome-modal', {backViewId: backViewId});


// back 的时候
var backHistoryId = $ionicHistory.currentHistoryId();
var backView = $ionicHistory.viewHistory().histories[backHistoryId].stack.filter(function (v) {
  return v.stateId === $stateParams.backViewId;
})[0];
$ionicHistory.backView(backView);
$ionicHistory.goBack();
```
