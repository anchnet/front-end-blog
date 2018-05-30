---
title: ES6 最佳实践系列一：let 和 const
date: 2017-10-15 19:03:12
tags:
- ES6
- 最佳实践
- 变量
- 常量
author: 小打
github: xiaoda
---

ES6 在 2015 年正式发布，2016 年在 Babel 的支持下迅速成为前端开发的主流<sup>[1]</sup>。ES6 使 JavaScript 这门语言变得更加正规、高级和高效。ES6 新特性非常多，边学边用的方式可能更适合大部分同学，把新特性应用到项目里能直观地体会到好处。“ES6 最佳实践”系列就是想和大家聊一聊 ES6 究竟如何改变了我们的代码。GoGo!

<!-- more -->

## let

ES6 新增了 let 命令，用来声明变量，用法类似于 var。不同的是，let 声明的变量只在代码块内（一对大括号）有效，解决了变量作用域的问题；let 不允许在一个作用域内重复声明同一个变量，避免了变量的重复定义和覆盖。

### 变量名称重复

过去，我们需要用变量名称来区分不同物品的同一个属性；

``` js
var num = 10
... // 处理逻辑

var num2 = 20
... // 另一个处理逻辑

console.log(num) // 20
```

现在，可以将每种物品的处理逻辑作为一个代码块，其中的变量名无需担心重复问题。

``` js
{
    let num = 10
    ... // 处理逻辑
}
{
    let num = 20
    ... // 另一个处理逻辑

    let num = 30 // Uncaught SyntaxError: Identifier 'num' has already been declared
}

console.log(num) // Uncaught ReferenceError: num is not defined
```

### 作用域

过去，需要用一个匿名函数来限制其中变量的作用域；

``` js
!function () {
    var item = 'A'
    ...
}()
```

现在，只需要一对大括号配合 let 就可以了。

``` js
{
    let item = 'A'
    ...
}
```

### 变量覆盖

经典案例，延时执行代码中的变量覆盖问题。let 很适合在 for 循环中使用。

``` js
var a = []
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i)
  }
}
a[5]() // 10
```

``` js
var a = []
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i)
  }
}
a[5]() // 5
```

### switch 中的使用

switch 语句中的 case 由于在语法上不需要大括号，无法获得变量作用域。如果在两个以上的 case 子句中用 let 声明了同一个变量会报错，此时需要手动添加大括号。

``` js
switch (exp) {
  case 'a': {
    let num = 10
    break
  }

  case 'b': {
    let num = 20
    break
  }
}
```

## const

ES6 新增了 const 命令，用来声明只读的常量。一旦声明，它的值就无法更改，这样避免了通用变量在全局使用中被意外更改和覆盖。const 特别适合用来声明引用的模块和配置<sup>[2]</sup>。

``` js
const path = require('path')
const MAX = 10

MAX = 99 // Uncaught TypeError: Assignment to constant variable.
```

const 的本质是变量指向的内存地址不得改动，因此简单类型数据（数值、字符串、布尔值）的值不会改变，复合类型的数据（主要是对象和数组）只能保证数据格式不变。冻结数组和对象的值应使用 [Object.freeze](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) 方法。

``` js
const foo = {}

foo.prop = 123
foo = {} // Uncaught TypeError: Assignment to constant variable.
```

## 注解

[1] 2017 年各大主流浏览器（Chrome / Firefox / Safari / IE Edge）对 ES6 标准的支持程度均达到 97% 左右，这意味着中后台、工具类项目可以使用原生的 ES6 代码；前台项目考虑到用户浏览器兼容性问题依然离不开 Babel 的预编译。
[2] 有同学认为只有在代码执行中真的会被改变的变量才应该使用 let 声明，其它都属于常量，应该使用 const 声明。个人认为很有道理，见仁见智。
