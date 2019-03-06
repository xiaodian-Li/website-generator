---
title: 安装包--save与 --save-dev
date: 2019-03-06 16:07:09
tags: [npm]
---
> #### tip1: 当拉下别人项目时 
> 
> npm i, npm装的依赖即有dependencies 也有devDependencies中的包
> 
> 
> #### tip2：当打包时
> 
> 使用--save安装的打包都打进去，
> 
> 使用--save-dev安装的不进行打包， 
> 
> 故打包大小就有区别，根据自己的需要进行选择--save 还是--save-dev
> 
> <!--more-->
> 
> eg: 安装webpack装在devDependencies中，使打包体积更小 

### npm i packagename 
* 加--save和不加--save区别在于
是否自动将package.json的依赖关系部分包含在包中  
* 装入dependencies套件中
### npm i packagename --save
* 简写--S 
* 装入dependencies套件中
* 打包计算在内
### npm i packagename --save-dev
* 简写--D
* 装入devDependencies套件中
* 打包不计算在内   


++默认情况下，NPM只是在node_modules下安装一个包。当您尝试为应用程序/模块安装依赖关系时，您需要先安装它们，然后将它们(以及相应的版本号)添加到package.json的依赖关系部分++

![image](http://static.daojia.com/sy/common/images/npm.png)