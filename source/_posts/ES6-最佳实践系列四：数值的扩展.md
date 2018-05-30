---
title: ES6 最佳实践系列四：数值的扩展
date: 2018-05-18 15:04:10
tags:
- ES6
- 最佳实践
- 数值
author: 小打
github: xiaoda
---

ES6 扩展了 Number 对象和 Math 对象的方法，使 JS 数值的操作更加强大和便利了。
主要特性：
    Number.isFinite()、Number.isNaN()、Number.parseInt()、Number.parseFloat()、
    Number.isInteger()、Math.trunc()、Math.sign()、指数运算符（\*\*）

<!-- more -->

### Number.isFinite()

该方法用来检查一个数是否有限；对非数值类型一律返回 false。因此，Number.isFinite() 非常适合用来检测变量是否为数值类型并有限。

``` js
Number.isFinite(123)      // true
Number.isFinite('123')    // false
Number.isFinite(Infinity) // false
```

### Number.isNaN()

Number.isNaN() 和传统的全局方法 isNaN() 不同。前者直接判断是否为 NaN，后者先将类型转换成数值类型再判断是否为 NaN。

``` js
Number.isNaN(NaN)   // true
Number.isNaN(123)   // false
Number.isNaN('123') // false

isNaN(NaN)   // true
isNaN(123)   // false
isNaN('123') // false
isNaN('abc') // true
```

### Number.parseInt() 和 Number.parseFloat()

ES6 将全局方法 parseInt() 和 parseFloat() 移植到 Number 对象上，功能保持不变。这样做的目的是逐步减少全局性方法，使 JS 语言逐步模块化。

``` js
Number.parseInt === parseInt     // true
Number.parseFloat === parseFloat // true
```

### Number.isInteger()

该方法用来判断一个数值是否为整数

``` js
Number.isInteger(123)  // true
Number.isInteger(1.23) // false
```

### Math.trunc()

该方法返回一个数的整数部分。

``` js
Math.trunc(1.23) // 1
```

### Math.sign()

该方法用来判断数的正负

``` js
Math.sign(123)  // 1
Math.sign(-123) // -1
Math.sign(0)    // 0
Math.sign(-0)   // -0

0 === -0 // true
```

### 指数运算符（\*\*）

与传统的指数运算方法（Math.pow()、Math.sqrt()）相比，指数运算符减少了算式代码的嵌套，提升了代码可读性。

``` js
2**2 === Math.pow(2, 2)    // true
2**0.5 === Math.sqrt(2, 2) // true
```
