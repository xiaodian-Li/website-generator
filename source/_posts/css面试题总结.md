---
title: css面试题总结
date: 2017-12-25 14:44:24
tags: [面试, css]
---
（以下是自己在网络上总结的css基础面试题）
### class和id有什么不同？
* id类名唯一，在页面中只能出现一次，更多地被用来实现宏伟布局和设计包含块，或包含框的样式。  
id是先确定页面的结构和内容，然后再为它定义样式  
* class类名不唯一，被多次调用，先确定样式在确定结构和内容<br>
<!--more-->
### CSS resetting和CSS normalizing 有什么不同？你倾向于使用哪种方案？
* normalize相对平和，注重通用方案，重置掉该重置的样式，保留有用的 user agent 样式，同时进行一些 bug 的修复，他是模块化的，有详细的文档
* Reset 相对暴力，不管你有没有用，统统重置成一样的效果，且影响的范围很大，讲求跨浏览器的一致性。 
几乎所有的元素施加默认样式
### 描述一下float，并解释一下它的作用方式？
float属性定义了元素是否浮动及在哪个方向浮动,在CSS中任何元素都可以浮动，且浮动元素会生成一个块级框，而不论它本身是何种元素。并且盒子的宽度不在伸展，而是根据盒子里面的内容的宽度来确定。  浮动属性会使得浮动的元素脱离文档流，所以文档的普通流中的块框会表现的像浮动框不存在一样
### 解释一下z-index和叠加上下文是如何形成的？
负边距 margin为负值时元素会依参考线向外偏移，没有计算好会折叠，position会发生折叠，且有z-index属性  
同级元素的z-index值如果相同，则堆叠顺序由元素在文档中的先后位置决定，后出现的会在上面，  
z-index值只决定同一父元素中的同级子元素的堆叠顺序。父元素的z-index值（如果有）为子元素定义了堆叠顺序（css版堆叠“拼爹”）
### 解释一下BFC（block formatting context）和工作原理？
* BFC（Block Formatting Context）直译为“块级格式化范围”
* 内部的Box会在垂直方向，一个接一个地放置。 
* Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
* BFC的区域不会与float box重叠。
* BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
* 计算BFC的高度时，浮动元素也参与计算  
用处：解决子元素浮动，父元素高度塌陷。  
两列自适应布局  
合并外边距
### clear属性有哪些？它有哪些适用场景？
clear 属性设置一个元素的侧面是否允许其他的浮动元素。  
left ：在左侧不允许浮动元素  
right ：在右侧不允许浮动元素  
both ：在左右两侧均不允许浮 动元素  
none：默认。允许浮动元素出现在两侧。  
当一个容器中的元素全部浮动之后，由于浮动会让元素脱离普通文档流，所以对于外面的这个容器来讲它就没有内容将它撑开，背景设置无法显示，margin设置无法显示。   
### CSS雪碧图是什么？如何实现？
译为“CSS图像拼合”或“CSS贴图定位”,  CSS Sprites就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。
* 优点：当页面加载时，不是加载每个单独图片，而是一次加载整个组合图片。这是一个了不起的改进，它大大减少了HTTP请求的次数，减轻服务器压力，同时缩短了悬停加载图片所需要的时间延迟，使效果更流畅，不会停顿。
* 缺点：做图像拼合的时候很麻烦。
### 你最喜欢的图片替换技术是什么？你会在什么时候使用？
设计师能够用一张背景图像替代某元素中的原始文字，以期显示出更美观的字体意义：而图像替换技术则保留了被替换元素中的原有文本，因此无论对何种客户而言，理解页面内容都不成问题。主要是考虑SEO，而非视觉上的效果。

### 如何处理特定浏览器的样式问题？
CSShack（利用了这些浏览器的漏洞价格，专门用这些漏洞来解决兼容性问题）:条件hack、属性级hack（_color:IE6；*color:IE7；color:#090\9:IE9）、选择符级hack3 （*html是IE6；*+html是IE7）
### 如何兼容某种功能受限的浏览器？
### 从视觉上将内容隐藏有哪些方式？（内容对屏幕阅读器可见）
display:none可以让网页中所有内容不显示  
visibility:hidden 被隐藏掉的内容仍旧占据空间  
overflow:hidden这种方式可以隐藏掉固定区域外的内容  
### 有没有使用过grid系统？如果用过，你喜欢哪个？
是CSS为布局新增的一个模块。网格布局特性主要是针对于Web应用程序的开发者。可以用这个模块实现许多不同的布局。网络布局可以将应用程序分割成不同的空间，或者定义他们的大小、位置以及层级。
### 是否使用过媒体查询或实现过特定移动端特定布局？
媒体查询，设置页面样式随屏幕宽度的变化而变化（IE8和IE8之前都不支持）
```
<meta name=“viewport” content=“width=device-width//可视窗口浏览器的宽度=设备的宽度（如果不加这句话在所有的移动端设备的宽度都是980）, initial-scale＝1.0, user-scalable=no//不允许用户缩放,maximum-scale=1.0//大的缩放系数, minimum-scale=1.0小的缩放系数”>
媒体查询 media queries：
@media screen:屏幕设备(手机、IPAD之类的)
@media print:打印机
@media projector:投影仪
@media screen and (min-width: 480px) and (max-width: 760px){
body{
1.CSS3 - Media Query（最简单的方式）
2.借助原生的JS（成本高，不推荐）
3.第三方开源框架 bootstrap（可以很好的浏览器响应式布局的设计）
 ```
em相对与父元素单位大小的；rem相对与html根元素单位大小的；
### 熟悉怎么为SVG设置样式吗？
矢量图形
### 如何优化网页进行打印？
@media print:打印机
### 为写出高性能的CSS，需要注意哪些陷阱？
![image](https://minisite.daojia.com/assets/img/imgcss1.png)  ![image](https://minisite.daojia.com//assets/img/imgcss6.png)  ![image](https://minisite.daojia.com//assets/img/imgcss3.png)

### CSS预处理器的优缺点是什么？描述你使用过的CSS预处理器中你喜欢的和不喜欢的地方？
预处理器例如：LESS、Sass、Stylus，用来预编译Sass或less，  
缺点：简单来说CSS预处理器语言较CSS玩法变得更高级了，但同时降低了自己对最终代码的控制力。提高了门槛，上手门槛，维护门槛，再来是团队整体水平和规范的门槛。这也造成了初学学习成本的昂贵。  
优点：增强了css代码的复用性， 还有层级、mixin、变量、循环、函数等，具有很方便的UI组件模块化开发能力，极大的提高工作效率  
### 如何实现使用了非标准字体的网页设计稿？
图片代替，  fonts在线字库，  网络字体fonticon使用字体图标
### 说明浏览器是如何确定和CSS选择器相匹配的元素的？
从后往前判断。符合就继续上一步，不符合就删除继续找
### 描述一下伪元素及它的用途？
![image](https://minisite.daojia.com//assets/img/imgcss4.png)
1、利用 after 清除浮动
```
.clearfix:after {content:"."; display:block; height:0; visibility:hidden; clear:both; } 
.clearfix { *zoom:1; }
```
2、伪元素与 css sprites 雪碧图  
3、作为列表序号  
4.超链接特效  
5.划线  
### 说明一下盒模型，怎么告诉浏览器使用不同的盒模型进行布局渲染？
标准盒模型与IE的怪异盒模型&弹性盒模型   IE怪异模式（无首行文档类型时）  
标准：width=content  
IE怪异模式：width=border+padding+content  
标准浏览器下模仿怪异盒模型  
box-sizing：border-box;
弹性盒模型  
box-flex是分配剩余空间，针对块级元素有效  
用<!DOCTYPE html>声明就是标准模式
### *{box-sizing: border-box;}什么意思？有什么优点？
相当于以怪异模式解析，border和padding全会在你设置的宽度内部。  
比如手机端设置两行并排的布局，宽度各为50%,如果不用这个属性，设置border后右边的div会下来错位，设置这个属性，宽度还是50%而不是50%+*px,两行可以并列显示
### 列举你所知道的display属性值？
![image](https://minisite.daojia.com//assets/img/imgcss5.png)
### inline和inline-block有什么区别？
inline：元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。  
设置宽高无效，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果； 但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。  
inline-block：将对象呈现为inline对象，但是对象的内容作为block对象呈现  
既具有block的宽度高度特性又具有inline的同行特性。  
### relative，fixed，absolute以及static的元素有什么区别？
static 默认  
relative相对定位（相对于自己的初始位置），空间不释放，未脱离原先的文档流。  
absolute绝对定位（相对于上一级已定位的父元素），空间释放，脱离文档流。  
fixed 固定定位（相对于浏览器），IE6及之前不支持。  
inherit 继承  
### 'C'代表级联。CSS最终规则是按什么优先级确定的？（能不能举一些例子）如何充分利用这些计算规则？
权重值：！important > 内联 > id（100） > class（10） >标签（1）  
css选择器： id class >（子代） ’ ‘（后代），（分组） ：（伪类） [ ]（属性）  
### 使用过哪些CSS框架？你是如何改变/改进它的？
Bootstrap两种动态css语言LESS和SASS，给css提供了变量，mixin，运算符等功能，让写出模块化的css框架成为可能
### 研究过CSS的新属性 flex和grid吗？
flex弹性布局flex | inline-flex  
当时设置flex布局之后，子元素的 float、clear、vertical-align 的属性将会失效。  
有下面六种属性可以设置在容器上，它们分别是：  
flex-direction ：决定主轴的方向(即项目的排列方向)  
flex-wrap：决定容器内项目是否可换行  
flex-flow ：flex-direction 和 flex-wrap 的简写形式  
justify-content：定义了项目在主轴的对齐方式。  
align-items：定义了项目在交叉轴上的对齐方式  
align-content：定义了多根轴线的对齐方式，如果项目只有一根轴线，那么该属性将不起作用  
grid-----见12题  
### 响应式设计和自适应设计有什么区别？
* 自适应是为了解决如何才能在不同大小的设备上呈现同样的网页
* 响应式正是为了解决自适应在小屏幕查看过于拥挤而衍生出来的概念。它可以自动识别屏幕宽度、并做出相应调整的网页设计，布局和展示的内容可能会有所变动。
### 有没有使用过retina图像？如果使用过，在什么场景下使用的什么技术？
 与几倍图有关
### 有没有必要使用translate替代绝对定位，反之亦然？ 为什么？
position 是为页面布局而生的。  
transform是为动画而生的,不会引起浏览器的重绘和重排。  
使用 position 时，最小的动画变化的单位是 1px而使用 transform 参与时，可以做到更小（动画效果更加平滑）










