---
title: 异步编程&事件循环event loops---总结
date: 2017-12-19 19:15:24
tags: [异步, js]
---
* js的执行环境是单线程的（一次只能完成一个任务），好处简单，坏处耗时长容易卡死。  
* 异步:是一个关于现在和将来的问题，现在执行的代码和将来执行的代码。在浏览器端，耗时很长的操作都应该异步执行，避免浏览器失去响应，最好的例子就是Ajax操作。  
下面代码如果同步，打印a的值是确认的；但是如果异步，a有两种可能（看哪个请求先回来）<br><!--more-->
```
var a = 1;
var b = 1;
 
function foo() {
    a = b + 3;
    console.log(a)
}
 
function bar() {
    b = a * 2;
}
 
ajax("url1", foo);
ajax("url2", bar);
```
异步编程的方法有：回调函数callback，事件监听，观察者---发布/订阅模式，Promise，Generator函数，async/await
#### 回调函数callback
假设有两种函数f1,f2。f2等待f1的结果，考虑把f2写成f1的回调f1(f2)  
回调函数的优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合，流程会很混乱，而且每个任务只能指定一个回调函数。
#### 事件监听
还是以f1,f2为例子
```
f1.on('done', f2);
```
这种方法的优点是比较容易理解，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以"去耦合"，有利于实现模块化。缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。
#### 观察者---发布/订阅模式
事件监听可以理解为信号，有一个信号中心，f1执行完就像信号中心发布一个信号，f2等其他任务可像信号中心订阅信号以知道自己什么时候可以开始执行。  
相当于f1执行完后，发出done信号，从而f2再执行。  
这种方法的性质与"事件监听"类似，但是明显优于后者。因为我们可以通过查看"消息中心"，了解存在多少信号、每个信号有多少订阅者，从而监控程序的运行。
#### promise对象
是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口。  
它的思想是，每一个异步任务返回一个Promise对象，该对象有一个then方法，允许指定回调函数。  
eg1:f1的回调函数f2,可以写成： 
```
f1().then(f2);
```
eg2:指定多个回调函数
```
f1().then(f2).then(f3);
```
eg3:指定发生错误时的回调函数
```
f1().then(f2).fail(f3);
```
这样写的优点在于，回调函数变成了链式写法，程序的流程可以看得很清楚，而且有一整套的配套方法，可以实现许多强大的功能。  
 如果一个任务已经完成，再添加回调函数，该回调函数会立即执行。所以，你不用担心是否错过了某个事件或信号。这种方法的缺点就是编写和理解，都相对比较难.
####  Generator函数
语法：
```
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}
let g = gen();
// "Generator { }"
```
方法
```
Generator.prototype.next()
返回一个由 yield表达式生成的值。
Generator.prototype.return()
返回给定的值并结束生成器。
Generator.prototype.throw()
向生成器抛出一个错误。
```
#### async异步/await等待
async 写在函数开头，代表异步，async和await一起使用，但是不一定非要有await，有await代表执行暂停  
当 async函数抛出异常时，Promise 的 reject方法将处理这个异常值。  
async 函数中可能会有 await 表达式，这将会使 async 函数暂停执行，等待 Promise 正常解决后继续执行 async 函数并返回解决结果。
async/awawit的简单使用.
```
function resolveAfter2Seconds(x) {
  return new Promise(resolve => { 
    setTimeout(() => {
      resolve(x); // 隔2秒执行resolve结果
    }, 2000);
  });
}
 
async function add1(x) {
  var a = resolveAfter2Seconds(20);
  var b = resolveAfter2Seconds(30);
  return x + await a + await b; // await 在一条语句，相当于2秒是平行进行
}
 
add1(10).then(v => { // async返回一个promise对象，return x + await a + await b === resolve(x + await a + await b)
  console.log(v);  // prints 60 after 2 seconds.
});
 
async function add2(x) {
  var a = await resolveAfter2Seconds(20); // await1执行完2秒
  var b = await resolveAfter2Seconds(30); // await2必须等await1执行完才执行，又花了2秒
  return x + a + b; // 共4秒
}
 
add2(10).then(v => {
  console.log(v);  // prints 60 after 4 seconds.
});
```
#### 事件循环event loops
循序大致都是先整体js,然后微任务（遇见宏任务task先做保留放在队列中-排队，不输出），宏任务 。  
简单插件asyncHelper，可以帮助我们异步的插入task和microtask。
```
//生成task
var myTask = asyncHelper.task(function () {
console.log('this is task')
});
//生成microtask
var myMicrotask = asyncHelper.mtask(function () {
console.log('this is microtask')
});
//插入task
myTask()
//插入microtask
myMicrotask();
```
常见的task（宏任务）任务源
- DOM 操作任务源：如元素以非阻塞方式插入文档
- 用户交互任务源：如鼠标键盘事件。用户输入事件（如 click） 必须使用 task 队列
- 网络任务源：如 XHR 回调
- history 回溯任务源：使用 history.back() 或者类似 API

- 事件回调
- XHR 回调
- IndexDB 数据库操作等 I/O
- setTimeout / setInterval
history.back

常见的microtask(微任务)任务源
- Promise.then
- MutationObserver
- Object.

![image](https://minisite.daojia.com/assets/img/image2017-12-13.png)
1每个 eventloop 由三个阶段构成：执行一个 task，执行 microtask 队列，可选的 ui render 阶段，requestAnimationFrame callback 在 render 阶段执行。我们平时写的逻辑代码会被分类为不同的 task 和 microtask。  
2.microtask 中注册的 microtask 事件会直接加入到当前 microtask 队列。  
3.microtask 执行时机『尽可能早』，只要 javascript 执行栈为空，就会执行。一轮 eventloop 中，可能执行多次 microtask。  
4.requestAnimationFrame callback 的执行时机与浏览器的 render 策略有关，是黑箱的

##### 小结考题
这样一段代码怎么的输出顺序
```
setTimeout(function(){
console.log('定时器开始啦')
});
new Promise(function(resolve){
console.log('马上执行for循环啦');
for(var i = 0; i < 10000; i++){
i == 99 && resolve();
}
}).then(function(){
console.log('执行then函数啦')
});
console.log('代码执行结束');
```
宏任务，微任务你理解么?
```
console.log('1');
setTimeout(function() {
console.log('2');
process.nextTick(function() {
console.log('3');
})
new Promise(function(resolve) {
console.log('4');
resolve();
}).then(function() {
console.log('5')
})
})
process.nextTick(function() {
console.log('6');
})
new Promise(function(resolve) {
console.log('7');
resolve();
}).then(function() {
console.log('8')
})
setTimeout(function() {
console.log('9');
process.nextTick(function() {
console.log('10');
})
new Promise(function(resolve) {
console.log('11');
resolve();
}).then(function() {
console.log('12')
})
})
```
执行顺序：整段代码，共进行了三次事件循环，完整的输出为1，7，6，8，2，4，3，5，9，11，10，12。  
macro-task(宏任务)：包括整体代码script，setTimeout，setInterval  
micro-task(微任务)：Promise，process.nextTick（callback）   

![image](https://minisite.daojia.com/assets/img/image2017-12-11.png)





<br>


> 参考文章
1.https://juejin.im/post/59e85eebf265da430d571f89  
2.https://github.com/aooy/blog/issues/5