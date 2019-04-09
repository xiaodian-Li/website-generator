---
title: '《现在前端技术技术解析》笔记一： web前端技术基础 '
date: 2019-04-09 18:53:46
tags: [前端基础]
---
### 1.Virtual DOM：  
用来描述页面DOM树节点之间关系的一种特殊JavaScript对象  
### 2.为了让用户尽可能快速看到内容？  
* 将一部分内容先展示给用户，然后根据用户的操作，异步加载用户需要的其他内容

* 如使用更高压缩比webp格式的图片

* 合理地利用文件缓存
<!--more-->
### 3.从我们打开浏览器输入一个网址到页面展示网页内容的这段时间内，浏览器和服务端都发生了什么事情？
* 在接收到用户输入的网址后，浏览器会开启一个线程来处理这个请求，对用户输入的URL地址进行分析判断，如果是HTTP协议就按照HTTP方式来处理。

* 调用浏览器引擎中的对应方法，比如WebView中的loadUrl方法，分析并加载这个URL地址。

* 通过DNS解析获取该网站地址对应的IP地址，查询完成后连同浏览器的Cookie、userAgent等信息向网站目的IP发出GET请求。

* 进行HTTP协议会话，浏览器客户端向Web服务器发送报文。

* 进入网站后台上的Web服务器处理请求，如Apache、Tomcat、Node.js等服务器。

* 进入部署好的后端应用，如PHP、Java、JavaScript、Python等后端程序，找到对应的请求处理逻辑，这期间可能会读取服务器缓存或查询数据库等。

* 服务器处理请求并返回响应报文，此时如果浏览器访问过该页面，缓存上有对应资源，会与服务器最后修改记录对比，一致则返回304，否则返回200和对应的内容。

* 浏览器开始下载HTML文档（响应报头状态码为200时）或者从本地缓存读取文件内容（浏览器缓存有效或响应报头状态码为304时）。

* 浏览器根据下载接收到的HTML文件解析结构建立DOM（Document Object Model，文档对象模型）文档树，并根据HTML中的标记请求下载指定的MIME类型文件（如CSS、JavaScript脚本等），同时设置缓存等内容。

* 页面开始解析渲染DOM，CSS根据规则解析并结合DOM文档树进行网页内容布局和绘制渲染，JavaScript根据DOM API操作DOM，并读取浏览器缓存、执行事件绑定等，页面整个展示过程[…]”

### 4. 浏览器内核主要指的就是渲染引擎
### 5.渲染树：
css样式  

1.布局：position， float， margin  

2.元素自身显示样式  

color， background， text-shadow  

### 6.DOM元素标签是指文本化的HTML标识，而DOM元素对象则是指经过渲染引擎DOM解析后生成的具有节点父子关系的树形对象
### 7.判断是否使用浏览器端文件缓存
1.cache-contorl 是否过期 （相对过期时间）  
没过期走缓存。  

过期判断  

2.是否有Etag，  

有 带if-None-Match去请求服务器  

没有  

3.判断是否有Last_Modified  

有 带if-Modified-Since去服务请求  

没有 向服务请求  

### 8.浏览器持久化缓存技术
1.使用浏览器多个标签页打开同个域名页面时，localStorage内容一般是共享的。  

2.sessionStorage和localStorage的功能类似，但是sessionStorage在浏览器关闭时会自动清空。  

3.Cookie的最大长度限制为4KB，和localStorage类似，不同域名之间的Cookie信息也是独立的  

4.Cookie分为两种：Session Cookie和持久型Cookie   

Session Cookie一般不设置过期时间，表示该Cookie的生命周期为浏览器会话期间，只要关闭浏览器窗口，Cookie就会消失  

Session Cookie一般不保存在硬盘上而是保存在内存里， 持久cookie保存在硬盘里  

### 9.Chrome的扩展功能
打开chrome://chrome-urls 查看chrome的扩展插件  

chrome://version/ //查看系统信息   
chrome://inspect/ //查看连接设备调试信息   
chrome://downloads //浏览器下载管理   
chrome://settings/ //浏览器设置 

