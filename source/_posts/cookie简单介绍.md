---
title: cookie简单介绍
date: 2017-11-16 17:53:21
tags: [cookie介绍,cookie使用,session]
categories: 前端知识
---

### cookie产生
1.因为http是无保留状态，所以才会用到cookie，
* 第一次客户端向服务端发送请求时，服务器端会生成cookie,
服务器端在响应中添加cookie返回，
* 第二次客户端向服务器端发送请求时，客户端携带cookie后发送，
服务器检查cookie，最后响应。<br><!--more-->
### cookie与session区别
* session机制在服务器端保持状态方案
cookie机制在客户端保持状态方案（会话跟踪机制)
*打开一次浏览器到关闭一次浏览器算一次会话*
### cookie分类
* 会话cookie
不设定它的生命周期expires时的状态,从打开到关闭浏览器，一个过程信息就会销毁
* 持久cookie
设定了它的生命周期expires,此时的cookie会有一个保质期，关了浏览器不会关闭，知道设定的过期时间，它可以在同一浏览器中传递数据，简单理解从首页登陆后到二级页面依然处于登陆状态，关了浏览器再打开依旧处于登陆状态
### 使用cookie
cookie的几种常见属性：document.cookie="key=value;expires=失效时间;path=路径;domain=域名;secure;(secure表安全级别）

<br>



