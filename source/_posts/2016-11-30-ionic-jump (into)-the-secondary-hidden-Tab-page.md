title: ionic 跳转（进入）二级页面隐藏Tab，无再进入第三季页面，TAB出现BUG
date: 2016-11-29 20:08:08
updated: 2016-11-30 20:08:08
tags:
	- Ionic
---

# 1.ion-view
在 `ion-view` 加上 `hide-tabs` 指令
```html
<ion-view hide-tabs>
..
</ion-view>
```

# 2.在JS中加入
```javascript
.directive('hideTabs', function ($rootScope, $location) {
    var style = angular.element('<style>').html(
      '.has-tabs.no-tabs:not(.has-tabs-top) { bottom: 0; }\n' +
      '.no-tabs.has-tabs-top { top: 44px; }');
    document.body.appendChild(style[0]);
    return {
      restrict: 'A',
      link: function (scope, element, attributes) {
        var tabBar = document.querySelector('.tab-nav');
        var scroll = element[0].querySelector('.scroll-content');
        scope.$on('$ionicView.beforeEnter', function () {
          scope.$watch(attributes.hideTabs, function (value) {
            tabBar.classList.add('slide-away');
            scroll.classList.add('no-tabs');
          });
        });
        scope.$on('$ionicView.afterLeave', function () {
          if ($location.path() == '/tab/aa_against' || $location.path() == '/tab/sf_against' || $location.path() == '/tab/yuding' || $location.path() == '/tab/mine') {
            tabBar.classList.remove('slide-away');
            scroll.classList.remove('no-tabs');
          }
        });
      }
    };
  });
```


# > PS：

在
```javascript
scope.$on('$ionicView.afterLeave', function () {}) 
```
加入
```javascript
if ($location.path()===···){}
```
判断是否为第一级页面,是才remove隐藏 `class` ，其他页面始终隐藏。
