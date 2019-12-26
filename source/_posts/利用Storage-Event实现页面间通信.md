---
title: 利用Storage Event实现页面间通信
date: 2018-07-26 15:29:36
tags: [localStorage]
categories: 存储
---
> 本文转自https://www.guoyunfeng.com/2018/07/22/storage-event/

我们都知道触发window.onstorage必须满足以下两个条件：  
  1. 通过localStorage.setItem或sessionStorage.setItem保存（更新）某个storage
  2. 保存（更新）这个storage时，它的新值必须与之前的值不同  
 <br><!--more-->
上面的第二个条件，简单来讲就是：要么是storage的初始化，因为不存在的storage，其值为null；要么就是对已有storage的更新 

举例：
```
// 初始化storage  
window.localStorage.setItem('a', 123);

// 注册onstorage事件
window.onstorage = (e) => {  console.log(e);
};

// 更新storage
window.localStorage.setItem('a', 123);
```
上面的最后一行代码并不会触发onstorage事件，因为a的值并没有变化，前后都是123，所以浏览器判定这次更新是无效的  

由于onstorage事件是浏览器触发的，所以如果我们打开了多个相同域名下的页面，并在其中任一一个页面执行window.localStorage.setItem方法（还要保证满足文章开头提到的第二个条件），那么其他页面如果监听了onstorage事件，则这些页面中的onstorage事件回调都会被执行  
举例：
```
// http://www.example.com/a.html
<script>
// 注册onstorage事件
window.onstorage = (e) => {  console.log(e);
}; 
</script>
```

```
// http://www.example.com/b.html
<script>
// 注册onstorage事件
window.onstorage = (e) => {  console.log(e);
};
</script>
```
```
// http://www.example.com/c.html
<script>
// 触发onstorage事件
window.localStorage.setItem('a', new Date().getTime());
</script>
```

只要保证c页面在a和b页面之后打开（哪怕三个页面不在同一浏览器窗口，这里需要区别窗口与tab页的区别），那么a和b页面中的onstorage事件都会被触发  

现在我们已经知道如何利用storage event实现了页面之间的通信，那么这个通信对于我们有何用途呢？
其实我们只需知道是哪个storage的更新操作触发了onstorage事件就足够了，那么我们如何知道呢？onstorage事件回调和其他事件回调函数一样，也接收一个event对象参数，在这个对象中有3个有用的属性，它们分别是：  
  1. key 被初始化或更新的storage的键名  
  2. oldValue被初始化或更新的storage之前的值  
  3. newValue被初始化或更新的storage之后的值  
结合这3个关键属性，我们就可以实现页面间的数据同步  

最后提一下localStorage与sessionStorage的区别

localStorage里面存储的数据没有过期时间设置，而存储在 sessionStorage里面的数据在页面会话结束时会被清除
