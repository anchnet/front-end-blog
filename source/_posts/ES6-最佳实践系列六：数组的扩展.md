---
title: ES6 最佳实践系列六：数组的扩展
date: 2018-06-01 11:36:55
tags:
- ES6
- 最佳实践
- 数组
author: 小打
github: xiaoda
---

ES6 扩展了数组。
主要特性：扩展运算符、Array.from()、Array.of()、find()、findIndex()、fill()、includes()

<!-- more -->

### 扩展运算符

扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

``` js
console.log(1, ...[2, 3]) // 1 2 3
```

由于扩展运算符可以展开数组，所以不再需要使用 apply 方法，将数组转为函数的参数了。

``` js
// 过去
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2]
f.apply(null, args)

// 现在
function f(x, y, z) {
  // ...
}
let args = [0, 1, 2]
f(...args)
```

另一个例子是通过 push 方法合并数组。

``` js
// 过去
var arr1 = [0, 1, 2]
var arr2 = [3, 4, 5]
Array.prototype.push.apply(arr1, arr2)

// 现在
let arr1 = [0, 1, 2]
let arr2 = [3, 4, 5]
arr1.push(...arr2)
```

### Array.from()

Array.from 方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

### Array.of()

Array.of 方法用于将一组值，转换为数组。

``` js
Array.of(1, 2) // [1, 2]
```

### 数组实例的 find() 和 findIndex()

数组实例的 find 方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。

``` js
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9
})
// 10
```

数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。

``` js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9
})
// 2
```

### 数组实例的 fill()

fill方法使用给定值，填充一个数组。过去只能用循环实现。

``` js
new Array(3).fill(7) // [7, 7, 7]
['a', 'b', 'c'].fill(7) // [7, 7, 7]
['a', 'b', 'c'].fill(7, 1, 2) // ['a', 7, 'c']
```

### 数组实例的 includes()

过去，我们只能通过 indexOf 方法判断一个数组是否包含给定的值。返回值与 -1 做比较在语义化方面非常差。

``` js
if ([1, 2].indexOf(1) > -1) {}
if ([1, 2].indexOf(1)) {} // 虽然符合直觉，但是不正确，出了问题很难发现。GG
```

现在，用 includes 方法可以轻松搞定。重要的是：返回值是布尔型！

``` js
if ([1, 2].includes(1)) {}
```
