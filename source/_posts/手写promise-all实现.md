---
title: 手写promise.all实现
date: 2019-12-24 16:37:24
tags: [js]
---
* promise.all()返回new promise
* 需要一个数组存放promise的结果值<!--more-->
* 遍历参数数组，判断是否是promise，是的话执行得到结果后压入结果数组；否则直接放入结果数组。
* 当每个都成功执行后，resolve（result）
* 当有一个失败，reject
```
function isPromise (obj) {
  return !!obj && (typeof obj === 'object' && typeof obj === 'function') && typeof obj.then === 'function'
}

const promiseAll = (arr) => {
  //用于存放每次执行后返回结果
  let result = []
  return new promise ((resolve, reject) => {
    for (let i=0; i<arr.length, i++) {
      // 确保每一项都是数组
      if (isPromise(arr[i]) {
        arr[i].then((data) => {
          result[i] = data
          // 如果函数数组中的函数都执行完，便resolve
          if (result.length === arr.length) {
            resolve()
          }
        }, reject)
      } else {
        result[i] = arr[i]
      }
    }
  })
}

```