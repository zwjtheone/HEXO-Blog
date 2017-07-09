title: javascript深入浅出系列-Array 之 实例方法汇总
date: 2017-06-23 21:57:13
tags:
  - javascript
---

# valueOf()

**valueOf()**返回数组本身

```
var arr = ["1","2","3"]
arr.valueOf();  // (3) ["1", "2", "3"]
```

# toString()

**toString()**返回数组的字符串形式,**注意，该方法不改变原数组**

```
var arr = ["1","2","3"]
arr.toString(); // 1,2,3
```

# join()

join方法以参数作为分隔符，将所有数组成员组成一个字符串返回。如果不提供参数，默认用逗号分隔,注意，该方法不改变原数组

```
var a = [1, 2, 3, 4];

a.join(' ') // '1 2 3 4'
a.join(' | ') // "1 | 2 | 3 | 4"
a.join() // "1,2,3,4"
```

与之对应的字符串转换成数组的方法是`split`

```
"1|2|3|4".split("|") // [1,2,3,4]
```

如果数组成员是undefined或null或空位，会被转成空字符串

```
[undefined, null].join('#')
// '#'

['a',, 'b'].join('-')
// 'a--b'
```

通过call方法，这个方法也可以用于字符串

```
Array.prototype.join.call('hello', '-')
// "h-e-l-l-o"
```

join方法也可以用于类似数组的对象

```
var obj = { 0: 'a', 1: 'b', length: 2 };
Array.prototype.join.call(obj, '-')
// 'a-b'
```

# concat()

concat方法用于多个数组的合并。它将新数组的成员，添加到原数组的尾部，然后返回一个新数组，原数组不变

```
['hello'].concat(['world'])
// ["hello", "world"]

['hello'].concat(['world'], ['!'])
// ["hello", "world", "!"]
```

除了接受数组作为参数，concat也可以接受其他类型的值作为参数。它们会作为新的元素，添加数组尾部

```
[1, 2, 3].concat(4, 5, 6)
// [1, 2, 3, 4, 5, 6]

// 等同于
[1, 2, 3].concat(4, [5, 6])
[1, 2, 3].concat([4], [5, 6])
```

如果不提供参数，concat方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是如果数组成员包括复合类型的值（比如对象），则新数组拷贝的是该值的引用

```
var obj = { a:1 };
var oldArray = [obj];

var newArray = oldArray.concat();

obj.a = 2;
newArray[0].a // 2
```

上面代码中，原数组包含一个对象，concat方法生成的新数组包含这个对象的引用。所以，改变原对象以后，新数组跟着改变。事实上，只要原数组的成员中包含对象，concat方法不管有没有参数，总是返回该对象的引用

concat方法也可以用于将对象合并为数组，但是必须借助call方法

```
[].concat.call({a: 1}, {b: 2})
// [{ a: 1 }, { b: 2 }]

[].concat.call({a: 1}, [2])
// [{a: 1}, 2]

[2].concat({a: 1})
// [2, {a: 1}]
```

# push()

**push**方法用于在数组的末端添加一个或多个元素，**并返回添加新元素后的数组长度。注意，该方法会改变原数组**

```
var arr = []
a.push(1) // 返回的是数组长度:1，  arr:[1]
a.push('a') // 返回的是数组长度:2，  arr:[1, 'a']
```

上面代码使用push方法，先后往数组中添加了2个成员。

如果需要合并两个数组，可以这样写

```
var a = [1, 2, 3];
var b = [4, 5, 6];

Array.prototype.push.apply(a, b) // 返回：6， a: [1,2,3,4,5,6]
// 或者
a.push.apply(a, b)  // 返回：6， a: [1,2,3,4,5,6]
// 或者使用
a.concat(b) // 注意concat直接返回合并之后的数组，不改变原有数组

// 上面两种写法等同于
a.push(4, 5, 6)

a // [1, 2, 3, 4, 5, 6]
```

# pop()

**pop**方法用于删除数组的最后一个元素，**并返回该元素。注意，该方法会改变原数组**

```
var a = ['1', '2', '3'];

a.pop() // '3'
a // ['1', '2']
```

对空数组使用pop方法，不会报错，而是返回undefined

```
[].pop() // undefined
```

>push和pop结合使用，就构成了“后进先出”的栈结构（stack）

# shift()

**shift**方法用于删除数组的第一个元素，**并返回该元素。注意，该方法会改变原数组**

```
var arr = [1,2,3]

arr.shift() // 返回删除的数组：1
console.log(arr) // [2,3]

var list = []
list.shift() // undefined
```

对空数组使用shift方法，不会报错，而是返回undefined

shift方法可以清空一个数组

```
var arr = [1, 2, 3, 4, 5, 6];
var item;

while (item = arr.shift()) {
  console.log(item);
}

arr // []
```

**push** 和 **shift**结合使用，就构成了“先进先出”的队列结构（queue）。

# unshift()

**unshift**方法用于在数组的第一个位置添加元素，**并返回添加新元素后的数组长度。注意，该方法会改变原数组**

```
var a = ['a', 'b', 'c'];

a.unshift('x'); // 4
a // ['x', 'a', 'b', 'c']
```

unshift方法可以在数组头部添加多个元素

```
var arr = [ 'c', 'd' ];
arr.unshift('a', 'b') // 4
arr // [ 'a', 'b', 'c', 'd' ]
```

如果合并数组可以这么写

```
var arr = [3,4]

Array.prototype.unshift.apply(arr,[1,2]) // 返回数组长度：4 , arr: [1,2,3,4]
或者
Array.prototype.unshift.call(arr,1,2) // 返回数组长度：4 , arr: [1,2,3,4]
或者
arr.unshift(1,2)
或者
arr.unshift.apply(arr,[1,2]) // 返回数组长度：4 , arr: [1,2,3,4]
或者
arr.unshift.call(arr,1,2) // 返回数组长度：4 , arr: [1,2,3,4]

```

# reverse()

**reverse**方法用于颠倒数组中元素的顺序，**返回改变后的数组。注意，该方法将改变原数组**

```
var a = ['a', 'b', 'c'];
a.reverse() // ["c", "b", "a"]
a // ["c", "b", "a"]
```

# slice()

**slice**方法用于提取原数组的一部分，**注意：返回一个新数组，原数组不变**

它的第一个参数为起始位置（从0开始），第二个参数为终止位置（**但该位置的元素本身不包括在内**）。如果省略第二个参数，则一直返回到原数组的最后一个成员

```
var a = ['a', 'b', 'c']

a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]
```

**上面代码中，最后一个例子slice没有参数，实际上等于返回一个原数组的拷贝。**

如果slice方法的参数是负数，则表示倒数计算的位置

```
var a = ['1', '2', '3'];
a.slice(-2) // ["2", "3"]
a.slice(-2, -1) // ["2"]
```

**上面代码中，-2表示倒数计算的第二个位置，-1表示倒数计算的第一个位置。**

如果参数值大于数组成员的个数，或者第二个参数小于第一个参数，则返回空数组。

```
var a = ['a', 'b', 'c'];
a.slice(4) // []
a.slice(2, 1) // []
```

slice方法的一个重要应用，是将类似数组的对象转为真正的数组

```
Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })
// ['a', 'b']

Array.prototype.slice.call(document.querySelectorAll("div"));
Array.prototype.slice.call(arguments); // 将方法参数转换成数组
```

上面代码的参数都不是数组，但是通过call方法，在它们上面调用slice方法，就可以把它们转为真正的数组

# splice()

**splice**方法对原数组进行增删改操作，用于删除原数组的一部分成员，并可以在被删除的位置添加入新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组

**splice**的第一个参数是删除的起始位置(包含此删除位置)，第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素

```
var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(4, 2) // ["e", "f"]
a // ["a", "b", "c", "d"]
```

上面代码从原数组4号位置，删除了两个数组成员

```
var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(4, 2, 1, 2) // ["e", "f"]
a // ["a", "b", "c", "d", 1, 2]
```

上面代码除了删除成员，还插入了两个新成员

起始位置如果是负数(负几就是倒数第几)，就表示从倒数位置开始删除

```
var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(-4,2) // ['c', 'd']
a // ['a','b','e','f']

```

上面代码表示，从倒数第四个位置c开始删除两个成员

如果只是单纯地插入元素，splice方法的第二个参数可以设为0

>第一个参数就是要插入的索引位置

```
var a = [1, 1, 1];

a.splice(1, 0, 2) // []
a // [1, 2, 1, 1] // 插入到索引1的位置


var a = ['a', 'b', 'c']

a.splice(a.length,0,2,3,4,5) // []
a // ["a", "b", "c", 2, 3, 4, 5]

相当于
a.push(2,3,4,5)
a // ["a", "b", "c", 2, 3, 4, 5]
```


如果只提供第一个参数，等同于将原数组在指定位置拆分成两个数组

```
var a = [1, 2, 3, 4];
a.splice(2) // [3, 4]
a // [1, 2]
```


更多[请参考](https://meiminjun.github.io/javascript-arr-splice)

# sort()

sort方法对数组成员进行排序，默认是按照字典顺序排序。**注意，排序后，原数组将被改变**

```
['d', 'c', 'b', 'a'].sort()
// ['a', 'b', 'c', 'd']

[4, 3, 2, 1].sort()
// [1, 2, 3, 4]

[11, 101].sort()
// [101, 11]

[10111, 1101, 111].sort()
// [10111, 1101, 111]
```

上面代码的最后两个例子，需要特殊注意。sort方法不是按照大小排序，而是按照对应字符串的字典顺序排序。也就是说，数值会被先转成字符串，再按照字典顺序进行比较，所以101排在11的前面。

如果想让sort方法按照自定义方式排序，可以传入一个函数作为参数，表示按照自定义方法进行排序。该函数本身又接受两个参数，表示进行比较的两个元素。如果返回值大于0，表示第一个元素排在第二个元素后面；其他情况下，都是第一个元素排在第二个元素前面。

```
[10111, 1101, 111].sort(function (a, b) {
  return a - b;
})
// [111, 1101, 10111]

[
  { name: "张三", age: 30 },
  { name: "李四", age: 24 },
  { name: "王五", age: 28  }
].sort(function (o1, o2) {
  return o1.age - o2.age;
})
// [
//   { name: "李四", age: 24 },
//   { name: "王五", age: 28  },
//   { name: "张三", age: 30 }
// ]
```

# map()

**map**方法对数组的所有成员依次调用一个函数，根据函数结果返回一个新数组,**注意，原数组不发生改变**

```
var numbers = [1, 2, 3];

numbers.map(function (n) {
  return n + 1;
});
// [2, 3, 4]

numbers
// [1, 2, 3]
```

上面代码中，numbers数组的所有成员都加上1，组成一个新数组返回

map方法接受一个函数作为参数。该函数调用时，map方法会将其传入三个参数，分别是**当前成员、当前位置索引和数组本身**

```
[1, 2, 3].map(function(elem, index, arr) {
  return elem * index;
});
// [0, 2, 6]
```

上面代码中，map方法的回调函数的三个参数之中，elem为当前成员的值，index为当前成员的位置，arr为原数组（[1, 2, 3]）

map方法不仅可以用于数组，还可以用于字符串，用来遍历字符串的每个字符。但是，不能直接使用，而要通过函数的call方法间接使用，或者先将字符串转为数组，然后使用

```
var upper = function (x) {
  return x.toUpperCase();
};

[].map.call('abc', upper)
// [ 'A', 'B', 'C' ]

// 或者
'abc'.split('').map(upper)
// [ 'A', 'B', 'C' ]
```

其他类似数组的对象（比如document.querySelectorAll方法返回DOM节点集合），也可以用上面的方法遍历。

map方法还可以接受第二个参数，表示回调函数执行时this所指向的对象

```
var arr = ['a', 'b', 'c'];

[1, 2].map(function(e){
  return this[e];
}, arr)
// ['b', 'c']
```

上面代码通过map方法的第二个参数，将回调函数内部的this对象，指向arr数组

如果数组有空位，map方法的回调函数在这个位置不会执行，会跳过数组的空位

```
var f = function(n){ return n + 1 };

[1, undefined, 2].map(f) // [2, NaN, 3]
[1, null, 2].map(f) // [2, 1, 3]
[1, , 2].map(f) // [2, , 3]
```

上面代码中，map方法不会跳过undefined和null，但是会跳过空位。

下面的例子会更清楚地说明这一点

```
Array(2).map(function (){
  console.log('enter...');
  return 1;
})
// [, ,]
```

上面代码中，map方法根本没有执行，直接返回了Array(2)生成的空数组

# forEach()

forEach方法与map方法很相似，也是遍历数组的所有成员，执行某种操作，但是forEach方法一般不返回值，只用来操作数据。如果需要有返回值，一般使用map方法

forEach方法的参数与map方法一致，也是一个函数，数组的所有成员会依次执行该函数。它接受三个参数，分别是当前位置的值、当前位置的编号和整个数组

上面代码中，forEach遍历数组不是为了得到返回值，而是为了在屏幕输出内容，所以应该使用forEach方法，而不是map方法，虽然后者也可以实现同样目的。

forEach方法也可以接受第二个参数，用来绑定回调函数的this关键字

```
var out = [];

[1, 2, 3].forEach(function(elem) {
  this.push(elem * elem);
}, out);

out // [1, 4, 9]
```

上面代码中，空数组out是forEach方法的第二个参数，结果，回调函数内部的this关键字就指向out。这个参数对于多层this非常有用，因为多层this通常指向是不一致的

```
var obj = {
  name: '张三',
  times: [1, 2, 3],
  print: function () {
    this.times.forEach(function (n) {
      console.log(this.name);
    });
  }
};

obj.print()
// 没有任何输出
```

上面代码中，obj.print方法有两层this，它们的指向是不一致的。外层的this.times指向obj对象，内层的this.name指向顶层对象window（详细解释参见《面向对象编程》一章）。这显然是违背原意的，解决方法就是使用forEach方法的第二个参数固定this

```
var obj = {
  name: '张三',
  times: [1, 2, 3],
  print: function () {
    this.times.forEach(function (n) {
      console.log(this.name);
    }, this);
  }
};

obj.print()
// 张三
// 张三
// 张三
```

注意，forEach方法无法中断执行，总是会将所有成员遍历完。如果希望符合某种条件时，就中断遍历，要使用for循环

```
var arr = [1, 2, 3];

for (var i = 0; i < arr.length; i++) {
  if (arr[i] === 2) break;
  console.log(arr[i]);
}
```

上面代码中，执行到数组的第二个成员时，就会中断执行。forEach方法做不到这一点

forEach方法与map方法一样会跳过数组的空位，forEach方法不会跳过undefined和null，代码如下：

```
var log = function (n) {
 console.log(n + 1);
};

[1, undefined, 2].forEach(log)
// 2
// NaN
// 3

[1, null, 2].forEach(log)
// 2
// 1
// 3

[1, , 2].forEach(log)
// 2
// 3
```

forEach方法也可以用于类似数组的对象和字符串

```
var obj = {
  0: 1,
  a: 'hello',
  length: 1
}

Array.prototype.forEach.call(obj, function (elem, i) {
  console.log( i + ':' + elem);
});
// 0:1

var str = 'hello';
Array.prototype.forEach.call(str, function (elem, i) {
  console.log( i + ':' + elem);
});
// 0:h
// 1:e
// 2:l
// 3:l
// 4:o
```

上面代码中，obj是一个类似数组的对象，forEach方法可以遍历它的数字键。forEach方法也可以遍历字符串

# filter()

filter方法的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。**注意，该方法不会改变原数组**

```
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

上面代码将大于3的原数组成员，作为一个新数组返回

filter方法的参数函数可以接受三个参数，第一个参数是当前数组成员的值，这是必需的，后两个参数是可选的，分别是当前数组成员的位置和整个数组

```
[1, 2, 3, 4, 5].filter(function (elem, index, arr) {
  return index % 2 === 0;
});
// [1, 3, 5]
```

上面代码返回偶数位置的成员组成的新数组

filter方法还可以接受第二个参数，指定测试函数所在的上下文对象（即this对象）

```
var Obj = function () {
  this.MAX = 3;
};

var myFilter = function (item) {
  if (item > this.MAX) {
    return true;
  }
};

var arr = [2, 8, 3, 4, 1, 3, 2, 9];
arr.filter(myFilter, new Obj())
// [8, 4, 9]
```

上面代码中，测试函数myFilter内部有this对象，它可以被filter方法的第二个参数绑定。上例中，myFilter的this绑定了Obj对象的实例，返回大于3的成员

# some()，every()

它们接受一个函数作为参数，所有数组成员依次执行该函数，返回一个布尔值。该函数接受三个参数，依次是当前位置的成员、当前位置的序号和整个数组

some方法是只要有一个数组成员的返回值是true，则整个some方法的返回值就是true，否则false

```
var arr = [1, 2, 3, 4, 5];
arr.some(function (elem, index, arr) {
  return elem >= 3;
});
// true
```

上面代码表示，如果存在大于等于3的数组成员，就返回true

every方法则是所有数组成员的返回值都是true，才返回true，否则false

```
var arr = [1, 2, 3, 4, 5];
arr.every(function (elem, index, arr) {
  return elem >= 3;
});
// false
```

上面代码表示，只有所有数组成员大于等于3，才返回true

注意，对于空数组，some方法返回false，every方法返回true，回调函数都不会执行

```
function isEven(x) { return x % 2 === 0 }

[].some(isEven) // false
[].every(isEven) // true
```

some和every方法还可以接受第二个参数，用来绑定函数中的this关键字

# [reduce()，reduceRight()](https://meiminjun.github.io/javascript-array-reduce)

reduce方法和reduceRight方法依次处理数组的每个成员，最终累计为一个值

它们的差别是，reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员），其他完全一样

这两个方法的第一个参数都是一个函数。该函数接受以下四个参数

1. 累积变量，默认为数组的第一个成员
2. 当前变量，默认为数组的第二个成员
3. 当前位置（从0开始）
4. 原数组

这四个参数之中，只有前两个是必须的，后两个则是可选的

下面的例子求数组成员之和

```
[1, 2, 3, 4, 5].reduce(function(x, y){
  console.log(x, y)
  return x + y;
});
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15
```

上面代码中，第一轮执行，x是数组的第一个成员，y是数组的第二个成员。从第二轮开始，x为上一轮的返回值，y为当前数组成员，直到遍历完所有成员，返回最后一轮计算后的x

利用reduce方法，可以写一个数组求和的sum方法

```
Array.prototype.sum = function (){
  return this.reduce(function (partial, value) {
    return partial + value;
  })
};

[3, 4, 5, 6, 10].sum()
// 28
```

如果要对累积变量指定初值，可以把它放在reduce方法和reduceRight方法的第二个参数

```
[1, 2, 3, 4, 5].reduce(function(x, y){
  return x + y;
}, 10);
// 25
```

上面代码指定参数x的初值为10，所以数组从10开始累加，最终结果为25。注意，这时y是从数组的第一个成员开始遍历

第二个参数相当于设定了默认值，处理空数组时尤其有用

```
function add(prev, cur) {
  return prev + cur;
}

[].reduce(add)
// TypeError: Reduce of empty array with no initial value
[].reduce(add, 1)
// 1
```

上面代码中，由于空数组取不到初始值，reduce方法会报错。这时，加上第二个参数，就能保证总是会返回一个值

下面是一个reduceRight方法的例子

```
function substract(prev, cur) {
  return prev - cur;
}

[3, 2, 1].reduce(substract) // 0
[3, 2, 1].reduceRight(substract) // -4
```

上面代码中，reduce方法相当于3减去2再减去1，reduceRight方法相当于1减去2再减去3

由于reduce方法依次处理每个元素，所以实际上还可以用它来搜索某个元素。比如，下面代码是找出长度最长的数组元素

```
function findLongest(entries) {
  return entries.reduce(function (longest, entry) {
    return entry.length > longest.length ? entry : longest;
  }, '');
}

findLongest(['aaa', 'bb', 'c']) // "aaa"
```

# indexOf(),lastIndexOf()

indexOf 方法返回给定元素在数组中第一次出现的位置索引，如果没有返回则返回-1,**注意，包含索引位置**

```
var a = [1,2,3,12,5,32,12]
a.indexOf(32) // 5
a.indexOf(11) // -1
```

indexOf 方法可以接受第二个参数，表示开始搜索的位置（**返回的值还是相对于原来数组的索引位置,不是从开始搜索位置的索引**）

```
var a = [1,2,3,12,5,32,12]
a.indexOf(2,2) // -1
a.indexOf(32,2) // 5
```

上面代码从1号位置开始搜索字符a，结果为-1，表示没有搜索到

lastIndexOf方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1

```
var a = [1,2,3,2,4,56,3,1,4]
a.lastIndexOf(3) // 6
a.lastIndexOf(33) // -1
```

注意，如果数组中包含NaN，这两个方法不适用，即无法确定数组成员是否包含NaN

```
[NaN].indexOf(NaN) // -1
[NaN].lastIndexOf(NaN) // -1
```

这是因为这两个方法内部，使用严格相等运算符（===）进行比较，而NaN是唯一一个不等于自身的值

# from()

Array.from() 方法从一个类似数组或可迭代的对象中重新创建一个新的数组实例，**注意：返回一个新数组，原数组不变**

```
const bar = ["a", "b", "c"];
var i = Array.from(bar); // ["a", "b", "c"]
bar === i // false

Array.from('foo');
// ["f", "o", "o"]
```

将NodeList 转化成 Array

```
var divs = Array.from(document.querySelectorAll('div'));

// Array[232] (every DIV on the page)
```

将 arguments 转化成 Array

```
function something() {
  var args = Array.from(arguments);

  // Array['yes', 1, {}]
}
something('yes', 1, {});
```

将 String 转化成 Array

```
Array.from('JavaScript'); // 很像'JavaScript'.split('')

// ["J", "a", "v", "a", "S", "c", "r", "i", "p", "t"]
```

与箭头函数搭配使用

```
Array.from([1, 2, 3], x => x + x);      
// [2, 4, 6]

Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

from 方法的第二个参数为可选参数，如果指定了该参数，则最后生成的数组会经过该函数的加工处理后再返回

如果传入第三个参数，执行第二个参数时，改变this 的指向

# 链式调用

上面这些数组方法之中，有不少返回的还是数组，所以可以链式使用

```
var users = [
  {name: 'tom', email: 'tom@example.com'},
  {name: 'peter', email: 'peter@example.com'}
];

users
.map(function (user) {
  return user.email;
})
.filter(function (email) {
  return /^t/.test(email);
})
.forEach(alert);
// 弹出tom@example.com
```

# 注意点

改变的原数组的几个方法，除此之外都不是：

* push()
* pop()
* shift()
* unshift()
* reverse()
* splice()
* sort()

不改变原数组：
* join()
* toString()
* concat()
* slice()
* map()
* forEach()
* filter()
* some()
* every()
* reduce()
* reduceRight()
* indexOf()
* lastIndexOf()
* from()
