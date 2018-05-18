---
title: pwa+lavas简述
date: 2018-05-17 11:45:16
tags: [性能, pwa, lavas]
categories: 前端知识
---
以下文章只是自己学习的小总结，“我不生产知识，我只是知识的搬运工。”
## PWA
### 1.首先，什么是pwa?  
Progressive Web App, 简称 PWA，是提升 Web App 的体验的一种新方法，能给用户原生应用的体验  <br><!--more-->
### 2.pwa的优点？  
PWA 本质上是 Web App，借助一些新技术也具备了 Native App 的一些特性，兼具 Web App 和 Native App 的优点。  
### 3.pwa的主要特点？  
* 可靠 - 即使在不稳定的网络环境下，也能瞬间加载并展现

1）当用户打开站点后，通过Service Worker 能让用户在网络很差的情况下也能瞬间加载展现  
2） 开发者可以预存储关键文件，淘汰过期文件，给用户提供可靠体验
* 体验 - 快速响应，并且有平滑的动画响应用户的操作

1） 页面在展现之后，有平滑的体验和过渡动画以及快速响应  
2）在内容请求完成后，优先保证App shell的渲染，做到和 Native App 一样的体验，App Shell 是 PWA 界面展现所需的最小资源。
* 粘性 - 像设备上的原生应用，具有沉浸式的用户体验，用户可以添加到桌面

1） 用户点击（pwa）可以安装到桌面，创建一个PWA应用，不需从应用商店下载  
2） 可以借助 Web App Manifest 提供给用户和 Native App 一样的沉浸式体验  
3） 可以通过给用户发送离线通知

### 4.pwa的特性？
* 渐进式 - 适用于所有浏览器，因为它是以渐进式增强作为宗旨开发的
* 连接无关性 - 能够借助 Service Worker 在离线或者网络较差的情况下正常访问
* 类似应用 - 由于是在 App Shell 模型基础上开发，因为应具有 Native App 的交互和导航，给用户 Native App 的体验
* 持续更新 - 始终是最新的，无版本和更新问题
* 安全 - 通过 HTTPS 协议提供服务，防止窥探和确保内容不被篡改
* 可索引 - 应用清单文件和 Service Worker 可以让搜索引擎索引到，从而将其识别为『应用』
* 粘性 - 通过推送离线通知等，可以让用户回流
* 可安装 - 用户可以添加常用的 webapp 到桌面，免去去应用商店下载的麻烦
* 可链接 - 通过链接即可分享内容，无需下载安装

### 5.PWA 改造的成本考虑
* 第一步，应该是安全，将全站 HTTPS 化，因为这是 PWA 的基础，没有 HTTPS，就没有 Service Worker
* 第二步，应该是 Service Worker 来提升基础性能，离线提供静态文件，把用户首屏体验提升上来
* 第三步，App Manifest，这一步可以和第二步同时进行
后续，再考虑其他的特性，离线消息推送等  

另外，PWA 采用的最新技术，当前浏览器还没有达到完全支持的程度。W3C 关于这些技术的标准也没有定稿。

> 关于更多pwa请查看pwa文档
https://lavas.baidu.com/doc


## LAVAS
### 1.什么是lavas?  
Lavas = Vue + PWA  

LAVAS基于 Vue.js 的 PWA 解决方案
帮助开发者快速搭建 PWA 应用，解决接入 PWA 的各种问题，
且开发者无须过多的关注 PWA 开发本身。  
### 2.学习lavas前提你需要掌握？
* HTML, CSS(less或stylus), JavaScript 等前端编程基础
* ES6/7 部分常用语法，如 Promise, import/export 等
* Vue, Vuex, Vue-router 等基本的开发知识 (教程、API 文档 和 编程风格指南)
* Webpack, Node.js 等基本知识 （推荐）  

### 3.Lavas 解决方案能够帮助开发者完成？
* 最基本的移动站点建设，包括 Vue, Vuex, Vue-router, webpack 等常用且成套的技术提供支持
* 允许站点添加至手机桌面，再次打开时全屏运行，摆脱浏览器的固定显示框架(地址栏，菜单栏等)
* 强化缓存，允许站点在弱网甚至离线的情况下继续显示内容
* 支持消息推送，帮助站长主动推送用户感兴趣的信息，提升业务指标
* 支持服务端渲染(SSR)，对搜索引擎更加友好
* 支持App Shell模型，在正常情况下提升加载性能，在异常情况下优化错误显示。   

### 4.Lavas 2.0新增功能？
* 服务端渲染 (SSR) 和浏览器端渲染 (SPA) 可以快速切换
* 自动生成路由规则，避免重复代码
* 针对 SSR 提供了更加合理的AppShell支持，享受更加顺滑和健壮的浏览体验

### 5.lavas基本命令？
###### (安装)
* 安装lavas命令行工具
```
npm i lavas -g
```
* 在所需的工程目录新建项目并命名
```
lavas init
```
* 进入项目安装依赖
```
npm i
```
* 启动开发服务器
```
lavas dev
lavas dev --port 8000 监听其他端口，eg:8000
```

###### (构建)
* 使用 Lavas 对项目进行构建(内部会调用 babel, webpack 等，最终生成在 /dist/ 目录中,可以通过 /lavas.config.js 进行修改)
```
lavas build
```
* lavas build 之后加入第三个参数以使用特定的配置文件进行构建，用以取代默认的 /lavas.config.js
```
lavas build config/lavas.another.config.js
```
###### (其他)
* 启动内置的正式服务器启动服务端渲染
```
build之后进入/dist/使用
npm i
lavas start
```
* 使用 Lavas 内置的静态服务器以当前目录为基准启动,(使用 localhost 访问即可预览带有 Service Worker 的站点效果)
```
用法：
1.在 构建后的 Lavas SPA 项目(默认 /dist/)启动
2.在任何其他目录启动

lavas static
```
<br>
> 关于更多lavas请查看lavas文档 https://lavas.baidu.com/guide

> 代码演练： https://lavas.baidu.com/codelab

> github地址： https://github.com/lavas-project/lavas