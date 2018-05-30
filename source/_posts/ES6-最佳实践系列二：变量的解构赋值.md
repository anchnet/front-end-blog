---
title: ES6 最佳实践系列二：变量的解构赋值
date: 2018-01-14 00:00:49
tags:
- ES6
- 最佳实践
- 解构赋值
author: 小打
github: xiaoda
---

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

<!-- more -->

### 赋值

过去，我们需要逐个取出数组或对象中的值赋值给变量；

``` js
var arr = [1, 2]
var obj = {c: 3, z: 4}

var a = arr[0]
var b = arr[1]
var c = obj.c
var d = obj.z
```

现在，可以一次将数组或对象中的值赋值给多个变量。

``` js
let [a, b] = [1, 2]
let {c, z: d} = {c: 3, z: 4}
```

### 默认值

给变量指定默认值变得更加简单和清楚。

``` js
// 过去
var a = arr[0] || 1
var b = arr[1] || 2
var c = obj.c || 3
var d = obj.z || 4
```

``` js
// 现在
let [a = 1, b = 2] = arr
let {c = 3, z: d = 4} = obj
```

### 函数参数

变量的解构赋值尤其适用于函数参数的定义。

``` js
// 过去
function test (options) {
    var defaultOptions = {a: 1}
    options = Object.assign(defaultOptions, options)

    console.log(options.a)
}
```

``` js
// 现在
function test ({a = 1, b} = {}) {
    console.log(a)
}
```

### 用途：交换变量的值

``` js
let a = 1
let b = 2

[a, b] = [b, a]
```
