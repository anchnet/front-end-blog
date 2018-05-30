---
title: ES6 最佳实践系列五：函数的扩展
date: 2018-05-30 15:24:32
tags:
- ES6
- 最佳实践
- 函数
author: 小打
github: xiaoda
---

ES6 扩展了函数。
主要特性：函数参数的默认值、rest 参数、箭头函数

<!-- more -->

### 函数参数的默认值

过去，我们只能在函数体中设定参数的默认值；

``` js
function log (x, y) {
  if (typeof x === undefined) x = 'Hello'
  if (typeof y === undefined) y = 'World'
  console.log(x, y)
}
```

现在，参数定义时就可以设定默认值，清晰明确，去掉参数时也不用担心函数运行报错。

``` js
function log (x = 'Hello', y = 'World') {
  console.log(x, y)
}
```

### rest 参数

过去，在函数内，我们用 arguments 对象（类数组对象）获取所有参数；现在可使用 rest 参数（数组）获取多余参数。

``` js
function add (x, ...values) {
  console.log(x, values)
}

add(1, 2, 3) // 1 [2, 3]
```

### 箭头函数

ES6 允许使用箭头定义函数。

``` js
let f = () => {}
let f = x => x
let f = (x, y) => {
  return x + y
}
```

注意点：
- 函数体内的 this 对象，是定义时所在的对象，而不是使用时所在的对象。
- 不可以当作构造函数（不可以使用 new 命令），否则会抛出一个错误。
- 不可以使用 arguments 对象，该对象在函数体内不存在。可使用 rest 参数代替。
- 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。
