---
title: font-size的可用单位有哪些？
date: 2019-02-21 11:58:26
tags: [css]
---
font-size的长度单位汇总如下：  
* 像素单位（px）
* em
* rem<!--more-->
* 百分比（%）
* 视窗单位（vw，vh，vmin，vmax）
* 绝对以及相对关键字设置字体大小（small,x-small等）
* 其他（英寸-in，厘米-cm等）<br>


就上面的长度单位，我们简单说一下：
### 1.像素单位（px）  
绝对长度单位。像素px是相对于显示器屏幕分辨率而言的，不支持IE的缩放

### 2.em   
相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸 
* em的值并不是固定的；
* em会继承父级元素的字体大小。 


++任意浏览器的默认字体高都是16px。所有未经调整的浏览器都符合: 1em=16px ；   
那么12px=0.75em,10px=0.625em  ；  
so,为了简化font-size换算，在body选择器中设置 Font-size=62.5%  ；  
这样em的值只需要将你的原来的px数值除以10，然后换上em作为单位就可以  
18px=1.8em, 10px=1em++

### 3.rem  
相对长度单位。使用rem为元素设定字体大小时，仍然是相对大小，但相对的是网页的根元素（html）元素  
关于rem的文章：http://www.alloyteam.com/2016/03/mobile-web-adaptation-tool-rem/

### 4.百分比（%）  
16px = 1em = 100% = 12pt  
单位换算网址：http://pxtoem.com/

### 5.vw  
视口百分比长度定义相对于viewport的大小的<length>值，即文档的可见部分。  
vw 代表视口宽度的 1/100。



> 参考：https://developer.mozilla.org/zh-CN/docs/Web/CSS/length