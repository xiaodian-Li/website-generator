---
title: Grid网格布局，了解一下？
date: 2019-06-17 21:18:27
tags: [css]
---
## Grid布局定义   
CSS的网格布局模块提供了一个基于网格的布局系统，能够以行和列来进行布局，使其更容易设计网页，而不必使用浮标和定位。  
只要给块级元素设置display:grid
或者给内联元素设置display:inline-grid，
Grid布局就可以创建
<!--more-->
## 先看一下效果  
display属性被设置为网格或内联网格。  

使用grid布局主要需要做的是将display设置为grid(块级元素)或inline-grid(内联元素)

```html
// grid-container称为grid容器
<div class="grid-container">
  // grid-item称为grid子项
  <div class="grid-item">1</div>
  <div class="grid-item">2</div>
  <div class="grid-item">3</div>  
  <div class="grid-item">4</div>
  <div class="grid-item">5</div>
  <div class="grid-item">6</div> 
</div>

<style>
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #2196F3;
  padding: 10px;
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  font-size: 30px;
  text-align: center;
}
</style>
```

![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG51_1560738512366.png)

## 主要属性介绍 
为了使一个HTML元素表现为一个网格容器，你必须设置显示属性为网格或内联网格。网格容器组成的网格项目，网格项目又置于行和列内。

#### grid-template-columns  

该属性定义的列数在网格布局，它可以定义每个列的宽度。其值是一个空格分隔列表，其中每个值定义的相应列的长度。  
css数据类型，表示网格容器内的灵活长度（如1fr,1.5fr)

> 注意：为了方便表示比例关系，网格布局提供了fr关键字（fraction 的缩写，意为"片段"）。如果两列的宽度分别为1fr和1.5fr，就表示后者是前者的1.5倍。

语法：  
```grid-template-columns: <track-size> ... | <line-name> <track-size>... ```
* <track-size>：宽度尺寸。可以是长度值，百分比值，以及fr单位（网格剩余空间比例单位）。
* <line-name>：自定义的命名。

```
.grid-container {
  display: grid;
  //网格布局有4列,所占宽度分别为50px 40px 30nepx 20px
  grid-template-columns: 50px 40px 30px 20px;
  //网格布局有5列,所占宽度分别如下
  grid-template-columns: 50px 40px 30px 20px 10px;
  // 容器分成3列，一列宽度为50px，然后将容器剩下的部分成2个部分,第二列和第三列各占1个部分
  grid-template-columns: 50px 1fr 1fr;
  // 自定义命名
  grid-template-columns: [第一纵线] 80px [纵线2] auto [纵线3] 100px [最后的结束线];
}
```
#### grid-template-rows
该属性定义每一行的高度。  
语法：  
```grid-template-rows: <track-size> ... | <line-name> <track-size> ... ```
* <track-size>：宽度尺寸。可以是长度值，百分比值，以及fr单位（网格剩余空间比例单位）。
* <line-name>：自定义的命名。

```
.grid-container {
  display: grid;
  // 网格布局有2行,所占高度分别如下80px 200px
  grid-template-rows: 80px 200px;
  // 容器分成3行，一行高度为50px，然后将容器剩下的高度分为2个部分,第二行和第三行高度各占1个部分
  grid-template-rows: 50px 1fr 1fr;
  // 任意命名
  grid-template-rows: [第一行开始] 25% [第一行结束] 100px [行3] auto [行4] 60px [行末];
}
```
#### justify-content
该属性用于横向对准容器内整个网格    
语法：
```
justify-content: stretch | start | end | center | space-between | space-around | space-evenly
```
可能取值  
* stretch：默认值。拉伸，宽度填满grid容器，拉伸效果需要网格目标尺寸设为auto时候才有效，如果定死了宽度，则无法拉伸。  
* space-evenly：evenly是匀称、平等的意思。也就是视觉上，每个flex子项两侧空白间距完全相等。   
* space-around：around是环绕的意思，意思是每个flex子项两侧都环绕互不干扰的等宽的空白间距，最终视觉上边缘两侧的空白只有中间空白宽度一半。   
* space-between：表现为两端对齐。between是中间的意思，意思是多余的空白间距只在元素中间区域分配。   
* center：表现为居中对齐。   
* start: 逻辑CSS属性值，与文档流方向相关。对齐容器的起始边框,默认表现为左对齐。   
* end：逻辑CSS属性值，与文档流方向相关。对齐容器的结束边框,默认表现为右对齐。

```
.grid-container {
  display: grid;
  justify-content: end;
}
```

space-evenly | space-around | space-between | center | start | end |
---|---|---|---|---|---
![](https://static.daojia.com/assets/project/tosimple-pic/1_1560824999398.jpg) | ![](https://static.daojia.com/assets/project/tosimple-pic/2_1560824999458.jpg) | ![](https://static.daojia.com/assets/project/tosimple-pic/3_1560824999457.jpg) | ![](https://static.daojia.com/assets/project/tosimple-pic/4_1560824999457.jpg) | ![](https://static.daojia.com/assets/project/tosimple-pic/5_1560824999369.jpg) | ![](https://static.daojia.com/assets/project/tosimple-pic/6_1560824999397.jpg)



#### align-content
该属性用于竖直地对准在容器内部的整个网格。  
语法：
```
align-content: stretch | start | end | center | space-between | space-around | space-evenly
```
可能取值
* stretch：默认值。每一行flex子元素都等比例拉伸。例如，如果共两行flex子元素，则每一行拉伸高度是50%。
* start： 逻辑CSS属性值，与文档流方向相关。默认表现为顶部开始。
* end： 逻辑CSS属性值，与文档流方向相关。默认表现为底部开始。
* center： 表现为整体垂直居中对齐。
* space-between: 上下两行两端对齐。剩下每一行元素等分剩余空间。
* space-around：
每一行元素上下都享有独立不重叠的空白空间。
* space-evenly：
每一行元素都完全上下等分。
```
.grid-container {
  display: grid;
  height: 400px;
  align-content: center;
}
```

#### place-content
该属性可以让align-content和justify-content属性缩写在一个CSS声明中
语法：
```
// 由于兼容性问题， 不建议合在一起
place-items: <align-content> / <justify-content>
```

## 网格间隙
每列/行之间的间隙被称为间隙
```
.grid-container {
  display: grid; // 网格布局
  grid-column-gap: 50px; // 列间距50px
  grid-row-gap: 10px; // 行间距10px
  grid-gap: 10px 50px ; // 分别设置行间距10px, 列间距50px
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG50_1560738319166.png)

## 网格线
列之间的线被称为列线。  
行之间的线被称为行线。
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG52_1560739613322.png)
#### 示例
放置在列线1的网格项目，并让它结束对列线3。  

可能取值：
```
grid-column-start: <number> | <name> | span <number> | span <name> | auto
```
<number>：起止于第几条网格线。  
<name>：自定义的网格线的名称。  
span <number>：当前网格会自动跨越指定的网格数量。  
span <name>：当前网格会自动扩展，直到命中指定的网格线名称。    
auto：全自动，包括定位，跨度等。
```css
.item1 {
  grid-column-start: 1;
  grid-column-end: 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG53_1560740516610.png)
#### 同理放在在排线(行线)1的网格项目，并让它结束对排线3
```css
.item1 {
  grid-row-start: 1;
  grid-row-end: 3;
}
```
#### grid-column（grid-column-start + grid-column-end）属性定义在其上的列（多个）放置的一个项目  
可能取值：
```
grid-column: <start-line> / <end-line> | <start-line> / span <value>;
```
eg:让item1在1号线开始和3号线结束：
```
.item1 {
  grid-column: 1 / 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG53_1560740516610.png)
eg:让item1开始在1号线开始和跨度3列结束：
```
.item1 {
  grid-column: 1 / span 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG55_1560742198725.png)
eg:让item1开始在2号线开始和跨度2列结束：
```
.item1 {
  grid-column: 2 / span 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG58_1560742987625.png)
#### grid-row（grid-row-start + grid-row-end）属性定义哪一行放置一个项目  
可能取值及原理同grid-column

## grid-area
该属性表示当前网格所占用的区域，可以被用作速记属性为 网格行启动，网格列启动，网格行截止和网格列截止的特性   

语法：
```
grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>
```
可能取值：
* <name>: 区域名称。由grid-template-areas属性创建。
* <row-start> / <column-start> / <row-end> / <column-end>:
占据网格区域的纵横起始位置。

eg:使“item1”上行线1和列线2开始，上行线4和列线3结束
```
.item1 {
  grid-area: 1 / 2 / 4 / 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG60_1560743684962.png)

eg:使“item1”对行线1和列2号线和跨度2行跨度3列结束
```
.item1 {
  grid-area: 1 / 2 / span 2 / span 3;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG62_1560750913864.png)

## 命名网格项目
grid-area属性也可以为网格项目Item命名
```
.item1 {
  // item1将被命名为“myArea”
  grid-area: myArea;
}
.grid-container {
  //item1跨越的3列网格布局所有3列：
  grid-template-areas: 'myArea myArea myArea';
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG64_1560751982883.png)

```
.item1 {
  // item1将被命名为“myArea”
  grid-area: myArea;
}
.grid-container {
  //item1跨越的5列网格布局中的3列
  grid-template-areas: 'myArea myArea myArea . . ';
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG65_1560752041895.png)
```
.item1 {
  grid-area: myArea;
}

.grid-container {
  // 让item1跨越两列和两行：
  grid-template-areas: 'myArea myArea . . .' 'myArea myArea . . .';
} 
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG66_1560752312852.png)


## 隐式网格
使用grid-auto-rows, grid-auto-columns, grid-auto-flow来设置隐式网格  
* grid-auto-rows：隐含创建的网格行的大小
* grid-auto-columns：隐含创建的网格列的大小轨道
* grid-auto-flow：隐含创建的网格的默认流方向
```
.grid-container {
  display: grid;
  background-color: #2196F3;
  padding: 10px;
  grid-gap:5px;
  // 行高度70px
  grid-template-rows: 70px;
  // 2列铺满各站1半
  grid-template-columns: repeat(2, 1fr);
  // 隐含创建的网格行的大小140px
  grid-auto-rows: 140px;
  // 隐含创建的网格的默认流方向: 行方向
  grid-auto-flow: row;
} 
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG69_1560759889368.png)

## Grid属性集

作用在grid容器上 | 作用在grid子项上
---|---
grid-template-columns（列宽） | grid-column-start
grid-template-rows（行高） |grid-column-end
grid-template-areas（命名网格） |grid-row-start
grid-template |grid-row-end
grid-column-gap（列间距）|grid-column
grid-row-gap |grid-row
grid-gap |grid-area
justify-items（水平呈现方式） |justify-self
align-items（垂直呈现方式）  |align-self
place-items （水平垂直呈现方式）|place-self
justify-content（水平分布方式） |
align-content（垂直方向的分布方式） |
place-content |
grid-auto-columns（隐式创建列大小） |
grid-auto-rows |
grid-auto-flow |
grid（网格布局）|

## Grid与Flex主要区别
* Grid布局则适用于更大规模的布局（二维布局），
处理一些不规则和非对称的设计。  
* Flexbox布局最适合应用程序的组件和小规模布局（一维布局）  


---
虽然grid存在一定的兼容（如下图），但是依照flex的趋势，grid的时代必然会来
![image](https://static.daojia.com/assets/project/tosimple-pic/1_1563245417637.png)



> 参考文章：   
> https://www.w3schools.com/css/css_grid.asp
> https://learncssgrid.com/








