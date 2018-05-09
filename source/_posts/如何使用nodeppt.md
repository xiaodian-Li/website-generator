---
title: 如何使用nodeppt
date: 2018-01-12 13:50:53
tags: [ppt分享]
categories: ppt
---
(演讲和分享的时候，怎么能让自己从不敢讲话到侃侃而谈，自信不胆怯是一方面，ppt也很重要哦，下面是一位好朋友分享给我的制作ppt)
### 首先nodePPT是基于markdown语法写的
* 几个常用的mark语法
<!--more-->
```
标题       h1到h6  
无序列表    * / - 
截断        <!--more-->
插入图片    ![image](相对或绝对地址)
表格eg:
|-----------|-----------|
| td | td | 
| td | td | 
引用         >文章
引用代码     ``<html>```  

```

### 创建文件夹
* 里面两个文件，通常是img和index
* 其中img放所需图片，index为markdown语法
### 进入index开始编写
title: 月度总结  
transition: 转场效  
//例如：zoomin/cards/slide  
theme:皮肤  
//例如：colors/moon/blue/dark/green/light 
highlightStyle: monokai_sublime  
//hljs的样式  
date: 2018年07月05日  
speaker: 李小点   
* [slide]用于分割每一页，
* 支持```<div></div>，<style></style>```
* [note][/note]用于标记备忘，多窗口时，只有自己能看见
### 启动PPT
* nodeppt start
### 导出ppt
1.导出html  
导出全部，包括nodeppt的js、img和css文件夹默认导出在publish文件夹  
```
nodeppt generate filepath -a
```
2.导出pdf  
使用url?print=1访问页面，然后选择chrome的系统打印即可：
打印 -> 使用系统对话框进行打印 -> (左下角)存储为PDF


> 参考文章https://github.com/ksky521/nodePPT












