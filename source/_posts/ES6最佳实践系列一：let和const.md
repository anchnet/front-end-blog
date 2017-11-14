---
title: ES6最佳实践系列一：let和const
date: 2017-10-15 19:03:12
tags:
author: 小打
---

ES6 在 2015 年正式发布，2016 年在 babel 的支持下迅速成为前端开发的主流。ES6 使 javascript 这门语言变得更加正规、高级和高效。ES6 新特性非常多，一时半会儿看不完，所以我选择了边做边学的方式一点一点学习 ES6 的大部分主要特性，应用到项目里并且直观地体会到它的好处。今天我想开这个“ES6最佳实践”系列说说 ES6 究竟如何改变了我们的代码。gogo!

## 1. let

ES6 新增了 let 命令，用来声明变量，用法类似于 var。不同的是，let 声明的变量只在代码块内（一对大括号）有效，解决了变量作用域的问题；let 不允许在一个作用域内重复声明同一个变量，避免了变量的重复定义和覆盖。过去我们需要用变量名称来区分不同物品的同一个属性；现在可以将每种物品的处理逻辑作为一个代码块，其中的变量名无需担心重复问题。

**过去：**

``` js
var num = 10
... // 处理逻辑

var num2 = 20
... // 另一个处理逻辑

console.log(num) // 20
```

**现在：**

``` js
{
    let num = 10
    ... // itemA 的处理逻辑
}
{
    let num = 20
    ... // itemB 的处理逻辑

    let num = 30 // Uncaught SyntaxError: Identifier 'num' has already been declared
}

console.log(num) // Uncaught ReferenceError: num is not defined
```

过去需要用一个匿名函数来限制其中变量的作用域，现在只需要一对大括号配合 let 就可以了。

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

经典案例，延时执行代码中的变量覆盖问题。let 很适合在 for 循环中使用。

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

switch 语句中的 case 由于在语法上不需要大括号，无法获得变量作用域。如果在两个以上的 case 子句中用 let 声明了同一个变量会报错。这时需要手动添加大括号。

``` js
switch (exp) {
  case 'a':
    {
      let num = 10
    }
    break

  case 'b':
    {
      let num = 20
    }
    break
}
```

## 2. const

ES6 新增了 const 命令，用来声明常量。一旦声明，它的值就无法更改。这样避免了全局、通用变量在使用中被意外更改和覆盖。const 特别适合用来声明引用的模块和配置。

``` js
const path = require('path')
const VISIBLE = true

VISIBLE = false // Uncaught TypeError: Assignment to constant variable.
```