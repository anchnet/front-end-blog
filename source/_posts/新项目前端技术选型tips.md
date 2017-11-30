---
title: 新项目前端技术选型 tips
date: 2017-11-30 11:22:24
tags:
author: 小打
---

在最近几年里，前端领域发展飞快。ES6/7/8 和 TypeScript 推动了语法的进步；Babel 让使用最新语法成为可能；Vue / React / Angular 提出了新的开发思维和方法；Webpack / Browserify 构建起了前端项目架构。渐渐的，前端被各领域的开发者们吐槽惨了<sup>[1]</sup>。面对质疑我不想做太多辩驳，只希望在看到前端复杂性的同时不要忽略前端愈发强大的能力。所有这一切归根结底都是工具，是提高生产力的辅助工具，对任何前端项目都不是强制必需，应该在有需要时选择使用。在这里我想为新项目的前端技术选型做一些粗浅的建议。

## 后端主导的项目

### 特点
1. 项目由后端工程师（php / python 等）主导。
2. 后端工程师的前端技术栈一般为：jQuery + 简单 css。
3. 注重功能实现、流程跑通，样式和交互够用即可。

### 推荐
* Bootstrap + jQuery

### 说明
1. 直接使用 Bootstrap 提供的 class 实现布局和样式，不需要自己写额外样式。
2. jQuery 实现前端功能，发送请求、操作 DOM。
3. GitHub 上有丰富的 jQuery 插件资源满足常规的前端需求如幻灯片、时间日期选择等。

## 前端主导的中后台项目

### 特点
1. 项目服务于内部用户（公司内部或开发者自己）。
2. 注重功能实现、流程跑通，样式和交互够用即可。
3. 不需要考虑旧浏览器的兼容性，在最新的浏览器上运行即可。
4. 技术选择自由，可根据开发者自身情况决定。
5. 性能要求不高，也没有 SEO 需求，项目架构可简配。

### 推荐
* ES6 + Vue / React + Element / Ant Design

### 说明
1. 浏览器（Chrome / Firefox / IE Edge）原生支持 ES6，轻松用上 ES6 特性。
2. 通过 script 标签引入 Vue / React，轻松用上框架。
3. Element / Ant Design 是基于 Vue / React 的组件库，快速搭建页面。

## 前端主导的前台项目

### 特点
1. 项目服务于外部用户。
2. 自定义的样式、交互需求，和功能实现同样重要。
3. 需要考虑旧浏览器及移动端浏览器的兼容性。
4. 性能要求高，可能有 SEO 需求，项目架构重要。

### 推荐
* ES6 / TypeScript + Vue / React + Webpack / Browserify + Babel

### 说明
1. TypeScript 有助于进一步规范 JS 变量类型，使代码逻辑易于理解。
2. Babel 预编译 JS 代码，解决浏览器兼容性问题。
3. 编写自定义样式、交互的 Vue / React 组件并复用。
4. 通过服务器端渲染、或以真实的 DOM 节点作为模板的方式使用 Vue，来满足 SEO 需求。
5. Webpack / Browerify 构建项目架构，配合插件满足项目的性能及其它要求。

## 注解

[1] 参考知乎文章 [在 2016 年学 JavaScript 是一种什么样的体验？](https://zhuanlan.zhihu.com/p/22782487?utm_medium=social&utm_source=qq) 和知乎问题 [2017年学JavaScript是一种什么体验？](https://www.zhihu.com/question/68716213)