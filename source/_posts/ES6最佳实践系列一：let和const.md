---
title: ES6最佳实践系列一：let和const
date: 2017-10-15 19:03:12
tags:
author: 小打
---

ES6 在 2015 年正式发布，2016 年在 babel 的支持下迅速成为前端开发的主流。ES6 使 javascript 这门语言变得更加正规、高级和高效。ES6 新特性非常多，一时半会儿看不完，所以我选择了边做边学的方式一点一点学习 ES6 的大部分主要特性，应用到项目里并且直观地体会到它的好处。今天我想开这个“ES6最佳实践”系列说说 ES6 究竟如何改变了我们的代码。gogo!

let 用来声明变量，类似于 var。不同的是，let 声明的变量只在代码块内（一对大括号）有效，有效地解决了变量作用域的问题。

曾经我们需要用变量名称来区分不同物品的同一个属性；现在可以将每种物品的处理逻辑作为一个代码块，其中的变量命名无需担心重复问题。

**过去：**

``` js
var itemANum = 10
... // itemA 的处理逻辑

var itemBNum = 50
... // itemB 的处理逻辑

var itemCNum = 100
... // itemC 的处理逻辑
```

**现在：**

``` js
{
    let num = 10
    ... // itemA 的处理逻辑
}
{
    let num = 50
    ... // itemB 的处理逻辑
}
{
    let num = 100
    ... // itemC 的处理逻辑
}
```

曾经需要用一个匿名函数来限制其中变量的作用域；现在只需要一对大括号就可以了。

**过去：**

``` js
!function () {
    var item = 'A'
    ...
}()
```

**现在：**

``` js
{
    let item = 'A'
    ...
}
```

经典案例，延时执行代码中的变量覆盖问题。

**过去：**

``` js
var a = []
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i)
  }
}
a[5]() // 10
```

**现在：**

``` js
var a = []
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i)
  }
}
a[5]() // 5
```

const 用来声明常量。一旦声明，它的值就无法更改。这样避免了全局的、通用的变量在使用中被意外更改、覆盖的情况。

``` js
const path = require('path')
const CONFIG = {}
```