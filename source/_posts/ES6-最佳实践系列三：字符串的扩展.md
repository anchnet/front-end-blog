---
title: ES6 最佳实践系列三：字符串的扩展
date: 2018-05-02 16:22:54
tags:
- ES6
- 最佳实践
- 字符串
author: 小打
github: xiaoda
---

ES6 加强了对 Unicode 的支持，并且扩展了字符串对象。
主要特性：includes()、startWith()、endsWith()、repeat()、padStart()、padEnd()、模板字符串等（\`\`）。

<!-- more -->

### includes()

过去，我们只能通过 indexOf 方法判断一个字符串是否包含另一个字符串。返回值与 -1 做比较在语义化方面非常差。

``` js
if ('hello'.indexOf('l') > -1) {}
if ('hello'.indexOf('l')) {} // 虽然符合直觉，但是不正确，出了问题很难发现。GG
```

现在，用 includes 方法可以轻松搞定。重要的是：返回值是布尔型！

``` js
if ('hello'.includes('l')) {}
```

### startsWith() 和 endsWith()

startsWith 和 endsWith 方法分别从头部、尾部搜索字符串。

``` js
'hello'.startsWith('h')
'hello'.endsWith('o')
```

### repeat()

过去，我们只能借助数组完成重复字符串的操作;

``` js
new Array(6).join('a') // 'aaaaa'
```

现在，用 repeat 方法可以轻松搞定。（个人更偏爱 ruby 和 python 的实现方法：'a'\*5，可惜 js 不支持）

``` js
'a'.repeat(5) // 'aaaaa'
```

### padStart() 和 padEnd()

padStart 和 padEnd 方法分别从头部、尾部补全字符串。

``` js
'18'.padStart(4, '2000') // '2018'
'1'.padEnd(3, 'st') // '1st'
```

### 模板字符串

过去，我们是这样定义模板的：

``` js
var name = 'xiaoda'
var age = 18
var tmpl = 'My name is ' + name + ', my age is ' + age // 'My name is xiaoda, my age is 18'
var tmpl2 = '\
    Fist Row\
    Second Row\
    Third Row\
'
```

现在，我们可以使用模板字符串。模板字符串在语义化方面非常棒。

``` js
let tmpl = `My name is ${name}, my age is ${age}` // 'My name is xiaoda, my age is 18'
let tmpl2 = `
    First Row
    Second Row
    Third Row
`
```
