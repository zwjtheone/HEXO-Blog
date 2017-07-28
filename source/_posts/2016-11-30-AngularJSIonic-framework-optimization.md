title: 基于AngularJS/Ionic框架开发的性能优化
date: 2016-11-30 12:31:00
updated: 2016-11-30 14:31:00
tags:
	- Ionic
	- Angular
---


下面提出几点优化的方法：

# 1. 使用单次绑定符号

```javascript
{{::value}}
```

AngularJS的性能优化方法之一是减少双向绑定。我们知道AngularJS的双向绑定是通过为每个需要双向绑定的数据对象添加$$watchers,一旦某个scope的数据发生了更新，
就触发脏检测($digest)，深度优先遍历所有scope对象的$$watchers值的old/new value是否发生变化。所以在开发过程中，我们都要小心判断创建出的每个$$watchers是否有必要。
对于只需要更新一次，以后不管数据层如何变化都不需要更新的数据，使用连续两个冒号即可在在$$watchers列表中将这个值删除，即减少了$digest脏检测循环。

# 2. ng-repeat优化

第一种方式虽然减少了脏检测的次数，但是单次绑定的数据毕竟少数，可能加完单次绑定，性能提升并没有太大。如果我们的代码中使用了ng-repeat,并且list数量很大时，
我们的性能会有很大下降，在移动端尤为明显。下面几点是对ng-repeat指令的优化。

使用limitTo来减少第一次加载列表元素的数量，以提高初始化页面的速度。我们也许有上百上千条数据要显示，但是屏幕的大小毕竟有限，
呈现在用户眼前的可能就是个1280x800或者360x640大小的屏幕，那我们可以先加载用户所能看到几个十几个列表。limitTo属性就提供了这样的功能。

```html
<li ng-repeat="mail in mails |limitTo:loadMailLimitTo"></li>
```

使用track by属性。比如我们有下面一段代码

```html
<ul>
    <li ng-repeat="mail in mails">
        {{mail.id}}:{{mail.title}}
    </li>
</ul>  
```

如果我们想更新mails里面的值，我们可能会这么做：

```javascript

$scope.mails = newMailListFromServer;

```

上一行代码会告诉ng-repeat去删除掉所有的li元素，再去重新生成一套新的li，这意味着大量的DOM操作，尤其当li元素里面有 复杂的逻辑判断和双向绑定数据。
这是因为ng-repeat在创建时会给每个mail加上$hashkey属性，并时时跟踪，一旦mails元素替换成服务器 返回的对象，即时他们完全一样，由于他们没有$hashkey,
所以ng-repeat不会知道他们是一样的元素。而通过如下的改动：


```html
<li ng-repeat="mail in mails track by mail.id"></li>
```

ng-repeat会跟踪我们创建的mail.id去判断是否为新的元素。这样就减少了大量的DOM删减添加操作。
需要注意的是，如果limitTo和track by一起使用的时候，需要把track by放到最后，如
```html

<li ng-repeat="mail in mails | limitTo:loadMailLimitTo track by mail.id"></li>

```

如果有引入ionic框架，可以使用collection-repeat替代ng-repeat。
collection-repeat是ionic框架自己的一套显示list的指令，原理在于不论list有多大，页面最多只有一定数量的item,这个item数量的大小是通过屏幕高度和单个item的高度计算出来的。
滑动列表时通过更新item元素的页面内容和位置来呈现所有的items。所以在大数量级的list呈现上，collection-repeat会比ng-repeat性能好很多。但是需要注意的是，
由于collection-repeat是通过时时更新滑动位置的item内容来实现的，所以在item内部使用第一个方法的单次绑定方式，滑动后会造成页面混乱的情况。

# 3. 减少html页面中的filter

原因是每当filter执行时，都会走两次$digest cycle，一次是scope中有数据改动，一次是查看是否有更多的改动需要更新数据。当数据量很大时对性能会有很大影响。
我们可以在初始化时就格式化好数据，比如赋值到view层之前，在我们的js代码里使用angular提供的$filter provider来预处理我们的数据。

# 4. ng-if替代ng-show/ng-hide

原因是ng-if与ng-show/ng-hide的不同之处在于，ng-if在等于false时会把元素从DOM中移除，所以所有绑在该元素上的handler会一同失效。
而ng-show/ng-hide不会移除DOM元素，而是使用css style去隐藏/显示DOM元素，所以handlers会一直存在。

# 5. $scope.$apply()和$scope.$digest()

我们会用到上面两种去执行一次脏检测，刷新页面数据。区别就是$scope.$apply()会从$rootscope开始，深度优先遍历执行$digest循环，
而$scope.$digest会从当前scope开始，往下层scope遍历脏检测。如果只是期望当前scope的数据更新，而不涉及到parent $scope，则可以使用$scope.$digest()。

# 6. angular animate

如果我们的项目引入了angular-animate.js的模块，那么在大部分使用了指令的元素上，animate里面的代码都会被执行，不管当前元素是否有应用css动画样式。
这对我们页面上如果有大量数据频繁滑动，隐藏显示的时候会有比较明显的性能问题。如果我们对当前scope并没有渐入渐出等动画效果的时候，
可以在当前scope初始化时加上$animate.enabled(false);当然，我们也可以对某个元素进行禁止动画的动作：$animate.enabled(element, false);

# 7. ionicSlideBox优化（只针对使用了ionic框架的项目）

初始化slidebox时先初始化显示中间的首先显示在用户面前的slide，其他的slide可以在$timeout里面延迟初始化。思想和ng-repeat的limitTo比较类似。
slidebox的滑动速度在ionic框架中默认速度是300ms滑完一个slide,通过改变这个速度来使滑动更快速。
