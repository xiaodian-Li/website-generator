---
title: Node学习随笔—http相关__URL模块
date: 2018-10-08 15:49:32
tags: [node, URL模块]
---
### 一：获取url地址中某一部分  
1.正则表达式  
2.url模块提供一些实例函数，用于URL处理和解析

### 二：具体api使用 
<!--more-->
http://nodejs.cn/api/url.html 

![](http://images.daojia.com/assets/other/images/gitimg/node-http2.png)

### 三：node中把url地址转为url对象  

WHATWG API解析一个URL字符串必须是完整的url

```
https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash
```

 url.parse 可以解析不是完整的url

```

let http = require('http') // 引入http模块

let url = require('url') 

http.createServer((req, res)={  // 创建连接

   console.log('req.url')  // 想取到url上hash必须转为对象

   let myurl = url.parse(req.url) // 对象

   console.log(myurl)

   console.log(myurl.search)

   res.end('服务终止')

}).listen(80, '127.0.0.1')

```



