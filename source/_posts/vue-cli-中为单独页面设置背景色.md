---
title: vue-cli 中为单独页面设置背景色
date: 2019-04-24 14:33:42
tags: [单页背景色]
---
背景：  
项目中6个页面，只有一个页面的背景为灰色（#f5f5f5）
eg: 
```
<template>
  <div class="orderDetail">
    <team-list class='customer-info' :item='item' :type='type'></team-list>
    <order-detail v-for='(each, index) in orderDetails' :item='each' 
                  @clickpark='clickPark' 
                  :componentType='componentType'>
    </order-detail>
  </div>
</template>
```
<!--more-->
方法1：  
直接在html中设置background-color：#f5f5f5
导致其他页面的背景色改变，所以不可取

方法2：  
最外层div-orderDetail设置position: fixed，脱离文档流,设置宽度高度100%，背景色#f5f5f5,
最后只是本页面改变，如果是长列表依旧不可以

方法3：  
在当前页面设置原生js方式，不影响全局，亲试符合需求可用
```
beforeCreate () {
   document.querySelector('body').setAttribute('style', 'background-color:#f5f5f5')
},
beforeDestroy() {
  document.querySelector('body').removeAttribute('style')
},
```

方法4：  
在全局路由钩子里,同样用原生js进行判断


