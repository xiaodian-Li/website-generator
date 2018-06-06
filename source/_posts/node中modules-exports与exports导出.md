---
title: node中modules.exports与exports导出
date: 2018-06-06 11:28:57
tags: [node, modules.exports/exports]
---
##### 一：node是什么？
node只是平台，或者说是环境，其实用的还是js语法  

主要框架express以及koa，两个框架是同一个团队开发，node中也有类似于php的Ci框架的MVC模式  
* M->model数据层的增删改差操作<br><!--more-->
* V->view视图层   
* C->controller路由控制，主要起到转发工作   

一个完整的node构成：node.js+express+mysql  

##### 二：工作代码的顺序：  
1. app.js为node的入口文件，  
1. 在view写好html文件，模板可以任意，  
1. rouer负责路由跳转  
1. controllers负责具体业务方法的操作，在这个文件里涉及到的增删改差放在model中  
1. model负责数据的操作    

此外，默认的端口号为3000，底层如启动命令也可以配置，node支持的导出为module.exports（整体导出） / exports（单个导出），模块引用为require  

##### 三：node中modules.exports与exports
node中使用require和modules.exports以及exports是因为node遵循CommonJS规范。

CommonJS定义的模块分为: 模块标识(module)、模块定义(exports) 、模块引用(require)
###### 使用范围
```require``` | ```export / import``` | ```module.exports / exports```
---|---|---|
node 和 es6 都支持的引入 | 只有es6 支持的导出引入| 只有 node 支持的导出  


exports与modules.exports指向相同地址  

```exports ->{}<- modules.exports```  

我理解为实际上每次都是导出```modules.exports```,本来指向一个地址，如下会切断```modules.exports```和```exports```分别指向两个地址  

```
a.js

modules.exports = {a:2}
exports.a = 1 
```
```
app.js

var a = require ('./a')
console.log(a.a) // 执行node app 打印2
```

###### 类比
```
var obj = new Object();
obj.name = 'lisi'


情况一：对象.属性
// obj.sayHello 相当于export.sayHello
obj.sayHello = function () {
    console.log(this.name) // lisi
}
obj.sayHello(); 


情况二：对象.方法
//obj相当于module.exports
obj = {
    sayHello: function () {
      console.log(this.name) // null
    }
}
obj.sayHello(); 
obj.name()； // 打印不出lisi,已经重写obj,obj下面没有name方法
```

此文章也是自己的学习记录，如有不足，欢迎指正知道


>更多文章： https://www.jianshu.com/u/f250f42cc28d


