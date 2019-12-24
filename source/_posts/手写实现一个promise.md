---
title: 手写实现一个promise
date: 2019-12-24 16:09:12
tags: [js]
---
* Promise是构造函数，new 出来的实例有then方法。
* new Promise时，传递一个参数，这个参数是函数，又被称为执行器函数(executor)， 并执行器会被立即调用，也就是上面结果中start最先输出的原因。
* executor是函数，它接受两个参数 resolve reject ，同时这两个参数也是函数。
* new Promise后的实例具有状态， 默认状态是等待，当执行器调用resolve后， 实例状态为成功状态， 当执行器调用reject后，实例状态为失败状态。
* promise翻译过来是承诺的意思，实例的状态一经改变，不能再次修改，不能成功再变失败，或者反过来也不行。
* 每一个promise实例都有方法 then ，then中有两个参数 ，我习惯把第一个参数叫做then的成功回调，把第二个参数叫做then的失败回调，这两个参数也都是函数，当执行器调用resolve后，then中第一个参数函数会执行。当执行器调用reject后，then中第二个参数函数会执行。
<!--more-->
```
function MyPromise (executor) {
  let self = this
  // 初始值
  self.value = undefined
  self.reason = undefined
  // 初始状态
  self.status = 'pending'
  // promise的then方法的第一参数，第二个参数
  self.resolvedCallback = []
  self.rejecteddCallback = []

  function resolve (value) {
    // 保证promise实例状态一旦变更不能再次改变，只有在pending时候才可以变状态
    if (self.status === 'pending') {
      self.value = value
      self.status = 'resolved'
      self.resolvedCallback.forEach(fn =>{
        fn()
      })
    }
  }

  function reject (reason) {
    if (self.status === 'pending') {
      self.reason = reason
      self.status = 'rejected'
      self.rejectedCallback.forEach(fn =>{
        fn()
      })
    }
  }

  executor(resolve, reject) // 立即执行两个函数
}


// new出来的实例具有then方法
MyPromise.prototype.then = function (onFullfilled, onRejected) {
  let self = this
  // 当执行器调用resolve后，then中第一个参数函数（成功回调）会执行,当执行器调用reject后，then中第二个参数函数（失败回调）会执行
  if (self.status === 'resolved') {
    onFullfilled(self.value)
  }
  if (self.status === 'rejected') {
    onFullfilled(self.reason)
  }
  if (self.status === 'pending') {
    self.resolvedCallback.push (function() {
      onFullfilled(self.value)
    })
    self.rejectedCallback.push (function() {
     onFullfilled(self.reason)
    })
  }
}

```
调用
```
let p = new MyPromise(function (resolve, reject) {
  console.log('start')
  setTimeout(function(){
      resolve('')
  },2000)
})
p.then(
  (v) => {
    console.log('success： ' + v)
  },
  (v) => {
    console.log('error： ' + v)
  }
)
p.then(
  (v) => {
    console.log('success： ' + v)
  },
  (v) => {
    console.log('error： ' + v)
  }
)
console.log('end')
```
执行结果为 ```start, end, success：data1,  success：data1```


> 参考链接：https://juejin.im/post/5c6ad98e6fb9a049d51a0f5e
