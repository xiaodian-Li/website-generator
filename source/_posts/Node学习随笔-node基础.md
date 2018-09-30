---
title: Node学习随笔--node基础
date: 2018-09-30 17:09:40
tags: [node, node基础]
---
1.浏览器输入网址发送请求，发生如下过程
![](http://images.daojia.com/assets/other/images/gitimg/node1.png)

客户端发送请求， www.baidu.com/www.taobao.com<br><!--more-->
到达服务器，服务器验证合法通过
根据请求需要，读取数据库
数据库经过统一封装，返回客户端
客户端接受数据，展示页面
2.V8引擎虚拟机解决性能
eg:谷歌因为是V8可以运行js，

特点：稳定高效

流程虚拟机，万能Js由来

放在服务器端，服务器端可以运行js------nnode.js

3.node.js
开始只能运行在客户端---》演变运行在服务端----》最后形成一个平台

只是平台（包装之后的v8引擎）不是语言，本身用的js语言

1.单线程

减少内存开销

2.非阻塞I/o

不会一直等，都会放在回调里

3.事件驱动

![](http://images.daojia.com/assets/other/images/gitimg/node2.png)

4.客户端与服务器
CS----pc客户端与服务端架构

BS----浏览器与服务端架构

url地址

![](http://images.daojia.com/assets/other/images/gitimg/node3.png)



![](http://images.daojia.com/assets/other/images/gitimg/node4.png)

5.http协议
请求

响应

6.exports与module.exports
本质的话是
let exports = module.exports
exports.name // 会改变module.exports
exports = {name：} // 会改变module.exports，{}改变创建了新的地址，改变指针指向

exports暴露的是方法属性exports.age="19"，.语法相当于没有创建新对象，指针指向没改变，如果={}的话，是创建了新的内存地址

同时exports也不支持输出类

module.exports暴露的是对象{}

module.exports包含exports

https://lixiaoyu.site/2018/06/06/node%E4%B8%ADmodules-exports%E4%B8%8Eexports%E5%AF%BC%E5%87%BA/#more

7.node.js-----Buffer（缓冲区）
容器--装二进制数据—类似于数组,怎么操作数组就可以怎么操作buffer

Buffer.form(string[, encoding])  string编码字符串， encoding编码类型

文件系统 fs 读入写出， 读入流写出流===掌握

8.数据库
对数据的管理，

分为关系型数据库（上）-----结构化，操作不灵活mySql

非关系型数据库（下） -------灵活，不适合大型数据的操作，适合微架构MongoDB

![](http://images.daojia.com/assets/other/images/gitimg/node5.png)

