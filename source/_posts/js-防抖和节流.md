---
title: js 防抖和节流
date: 2019-12-24 17:01:02
tags: [js]
---
防抖：事件被触发n秒后再执行，n秒内重新触发重新计时  
应用场景：搜索、调整窗口大小  
<br><!--more-->
```
function debounce (fn, wait, immediate) {
  let timer = null

  return function () {
    let context = this
    let args = arguments
    if (immediate) {
      fn.call(context, ...args)
      immediate = false
    }

    clearTimeout(timer)
    timer = setTimeout(function(){
      fn.call(context, ...args)
    }, wait)
  }

}
```



节流： 一个函数N秒内只执行一次  
应用场景：监听滚动事件、鼠标不断点击触发  
```
function throttle (fn, wait, immediate) {
  let timer = null
  return function () {
    let context = this
    let args = arguments
    if (immediate) {
      fn.call(context, ...args)
      immediate = false
    }

    // 如果当前存在定时器，返回；否则设置定时器
    if (timer) return 
    timer = setTimeout(function(){
      fn.call(context, ...args)
      // 函数执行完毕后，清除定时器
      clearTimeout(timer)
      timer = null
    }, wait)
  }
}
```