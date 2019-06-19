---
title: Grid网格布局，了解一下？
date: 2019-06-17 21:18:27
tags: [css]
---
## 1.Grid布局定义  
CSS的网格布局模块提供了一个基于网格的布局系统，能够以行和列来进行布局，使其更容易设计网页，而不必使用浮标和定位。  
## 2.网格布局创建  
display属性被设置为网格或内联网格。  
块级元素设置display:grid  
内联元素设置display:inline-grid
<!--more-->
```html
<!-- grid-container称为grid容器 -->
<div class="grid-container">
  <!-- grid-item称为grid子项 -->
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

## 3.网格容器
为了使一个HTML元素表现为一个网格容器，你必须设置显示属性为网格或内嵌网格。  
网格容器组成的网格项目，置于行和列内。

##### 3-1.grid-template-columns属性定义的列数在网格布局，它可以定义每个列的宽度。  
该值是一个空格分隔列表，其中每个值定义的相应列的长度。  
css数据类型，表示网格容器内的灵活长度（如1fr,1.5fr)
```
.grid-container {
  display: grid;
  //网格布局有4列,所占宽度分别为50px 40px 30px 20px
  grid-template-columns: 50px 40px 30px 20px;
  //网格布局有5列,所占宽度分别如下
  grid-template-columns: 50px 40px 30px 20px 10px;
  // 容器分成3列，一列宽度为50px，然后将容器剩下的部分成2个部分,第二列和第三列各占1个部分
  grid-template-columns: 50px 1fr 1fr;
}
```
##### 3-2.grid-template-rows属性定义每一行的高度。
```
.grid-container {
  display: grid;
  // 网格布局有2行,所占高度分别如下80px 200px
  grid-template-rows: 80px 200px;
  // 容器分成3行，一行高度为50px，然后将容器剩下的高度分为2个部分,第二行和第三行高度各占1个部分
  grid-template-rows: 50px 1fr 1fr;
}
```
##### 3-3.justify-content属性用于横向对准容器内整个网格  
可能取值  
* stretch：默认值。拉伸，宽度填满grid容器，拉伸效果需要网格目标尺寸设为auto时候才有效，如果定死了宽度，则无法拉伸。  
* space-evenly：evenly是匀称、平等的意思。也就是视觉上，每个flex子项两侧空白间距完全相等。   
* space-around：around是环绕的意思，意思是每个flex子项两侧都环绕互不干扰的等宽的空白间距，最终视觉上边缘两侧的空白只有中间空白宽度一半。   
* space-between：表现为两端对齐。between是中间的意思，意思是多余的空白间距只在元素中间区域分配。   
* center：表现为居中对齐。   
* start：默认值。逻辑CSS属性值，与文档流方向相关。默认表现为左对齐。   
* end：逻辑CSS属性值，与文档流方向相关。默认表现为右对齐。

```
.grid-container {
  display: grid;
  justify-content: end;
}
```

space-evenly | space-around | space-between | center | start | end |
---|---|---|---|---|---
![](https://static.daojia.com/assets/project/tosimple-pic/411560512492__1560512669908.pic) | ![](https://static.daojia.com/assets/project/tosimple-pic/421560512520__1560512671284.pic) | ![](https://static.daojia.com/assets/project/tosimple-pic/431560512545__1560512673274.pic) | ![](https://static.daojia.com/assets/project/tosimple-pic/441560512563__1560512674646.pic) | ![](https://static.daojia.com/assets/project/tosimple-pic/451560512594__1560512676121.pic) | ![](https://static.daojia.com/assets/project/tosimple-pic/461560512610__1560512983075.pic)



##### 3-4.align-content属性用于竖直地对准在容器内部的整个网格   
可能取值stretch，space-evenly，space-around，space-between，center，start，end （同justify-content取值）
```
.grid-container {
  display: grid;
  height: 400px;
  align-content: center;
}
```

##### 3-5.place-content可以让align-content和justify-content属性缩写在一个CSS声明中
```
.container {
    // 由于兼容性问题， 不建议合在一起
    place-items: <align-content> / <justify-content>;
}
```
## 4.网格间隙
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

## 5.网格线
列之间的线被称为列线。  
行之间的线被称为行线。
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG52_1560739613322.png)
##### 5-1.放置在列线1的网格项目，并让它结束对列线3
可能取值：
```
grid-column-start: <number> | <name> | span <number> | span <name> | auto
```
<number>：起止与第几条网格线。  
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
##### 5-2.同理放在在排线(行线)1的网格项目，并让它结束对排线3
```css
.item1 {
  grid-row-start: 1;
  grid-row-end: 3;
}
```
##### 5-3.grid-column（grid-column-start + grid-column-end）属性定义在其上的列（多个）放置的一个项目  
可能取值：
```
grid-column: <start-line> / <end-line> | <start-line> / span <value>;
```
eg:让item1开始在1号线和3号线结束：
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
  grid-column: 2 / span 2;
}
```
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG58_1560742987625.png)
##### 5-4.grid-row（grid-row-start + grid-row-end）属性定义哪一行放置一个项目  
可能取值及原理同grid-column

## 6.grid-area属性可以被用作速记属性为 网格行启动，格列启动，网格行端和网格列端的特性

eg:使“item1”上行线1和列线2开始，上行线4和列线6结束
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

## 7.命名网格项目
grid-area属性也可用于分配的名称并网项目
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
![image](https://static.daojia.com/assets/project/tosimple-pic/WechatIMG66_1560752312852.png )

## 8.隐式网格
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

## 9.Grid属性集

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

## 10.Grid与Flex主要区别
* Grid布局则适用于更大规模的布局（二维布局），
处理一些不规则和非对称的设计。  
* Flexbox布局最适合应用程序的组件和小规模布局（一维布局）  

* 2D 布局适合使用 CSS grids（行与列）  
* Flexbox 适用于单一维度的布局（行或列）

虽然grid存在一定的兼容，但是依照flex的趋势，grid的时代必然会来


> 参考文章  
> https://www.w3schools.com/css/css_grid.asp
> https://learncssgrid.com/





