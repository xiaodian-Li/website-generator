---
title: Node学习随笔—http相关__http模块与路由
date: 2018-10-08 15:48:14
tags: [node, http模块,路由]
---
## 一：http模块  
http模块是node的常用模块，可以用浏览器访问写的代码

1.引进http模块（核心模块不需要安装）
```
 let http = require("http")
```

2.创建服务器（参数接受函数）<br><!--more-->
```
 let server = http.createServer((req, res)=>{
	// 返回结果（状态码，返回类型， 返回的编码）
	res.writeHead(200,{"Content-type": "text/html"; charset=UTF-8})
	// 浏览器内容
	res.write("111")
	res.write("<h1>哈哈哈哈哈</h1>")
	res.end("hello")
})

```
3.监听(知道访问，参数端口号，地址locallhost)
```
server.listen(80, "127.0.0.1")
```

## 二：路由  
1.node只能通过控制url来控制跳转，在服务器端先配置好路由  

2.配置路由  

引入读写操作文件
```
let fs = require（fs）
```
```

 let server = http.createServer((req, res)=>{
	if (req.url==='/test1.html') { // 浏览器地址栏的路由url
		console.log(111)
		// 读入文件
		fs.readFile("./test1.html", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "text/html"; charset=UTF-8})
				res.end(data)
			}
		})
	} else if (req.url==='/test2.html') {
		console.log(222)
		// 读入文件
		fs.readFile("./test2.html", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "text/html"; charset=UTF-8})
				res.end(data)
			}

		})
	} else if (req.url==='/') {


	}else {
		// 返回结果（状态码，返回类型， 返回的编码）
		res.writeHead(404,{"Content-type": "text/html"; charset=UTF-8})
		// 浏览器内容
		res.end("访问页面不存在")
	}
})

```
3.node中加载其他类型资源

---除了html和js文件除外的类型文件的访问

比如css文件，img图片， 音频等，要用fs读到服务中如下
```
 let server = http.createServer((req, res)=>{
	if (req.url==='/test1.html') { // 浏览器地址栏的路由url， 路由1
		console.log(111)
		// 读入文件
		fs.readFile("./test1.html", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "text/html"; charset=UTF-8})
				res.end(data)
			}
		})
	} else if (req.url==='/test2.html') { // 浏览器地址栏的路由url， 路由2
		console.log(222)
		// 读入文件
		fs.readFile("./test2.html", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "text/html"; charset=UTF-8})
				res.end(data)
			}

		})
	} else if (req.url==='/css/index/.css') { // css
		// 读css文件
		fs.readFile("./css/index/.css", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "text/css"}) // text/css
				res.end(data)
			}
		})
	}else if (req.url==='/img/lixiaoyu.png') { // 图片
		// 读图片文件
		fs.readFile("./img/lixiaoyu.png", (err, data)=>{
			if (!err){
				console.log(data.toString)
				res.writeHead(200,{"Content-type": "image/jpg"}) // image/jpg
				res.end(data)
			}
		})
	} else {
		// 返回结果（状态码，返回类型， 返回的编码）
		res.writeHead(404,{"Content-type": "text/html"; charset=UTF-8})
		// 浏览器内容
		res.end("访问页面不存在")
	}
})

```
小节图如下：![](http://images.daojia.com/assets/other/images/gitimg/node-http1.png)



