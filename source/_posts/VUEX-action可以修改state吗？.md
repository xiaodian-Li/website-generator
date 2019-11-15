---
title: VUEX-action可以修改state吗？
date: 2019-11-15 11:42:49
tags: [vue, vuex]
---
### 首先回顾下vuex，官网图如下：
![image](https://static.daojia.com/assets/project/tosimple-pic/vuexstate_1573783585247.png)
<!--more-->
* Vuex 的 store 中的状态的唯一方法是提交 mutation（mutation类似于事件且必须是同步函数）  
* action 提交的是 mutation，而不是直接变更状态且可以包含任意异步操作（Action通过 store.dispatch 方法触发）

### 一幅图看清只能通过mutation修改state的原因：
![image](https://static.daojia.com/assets/project/tosimple-pic/vuexstateexplain_1573784451155.png)
* commit函数源码如下
```
 commit (_type, _payload, _options) {
    // check object-style commit
    const {
      type,
      payload,
      options
    } = unifyObjectStyle(_type, _payload, _options)

    const mutation = { type, payload }
    const entry = this._mutations[type]
    if (!entry) {
      if (process.env.NODE_ENV !== 'production') {
        console.error(`[vuex] unknown mutation type: ${type}`)
      }
      return
    }
    // 用来修改state
    this._withCommit(() => {
      entry.forEach(function commitIterator (handler) {
        handler(payload)
      })
    })
    this._subscribers.forEach(sub => sub(mutation, this.state))

    if (
      process.env.NODE_ENV !== 'production' &&
      options && options.silent
    ) {
      console.warn(
        `[vuex] mutation type: ${type}. Silent option has been removed. ` +
        'Use the filter functionality in the vue-devtools'
      )
    }
  }
  ```
  * this._withCommit来修改state，其源代码如下
  ```
 _withCommit (fn) {
    const committing = this._committing
    this._committing = true
    fn()
    this._committing = committing
  }
  ```
  * 其中```_withCommit```函数的参数fn是修改state的函数，在执行fn函数前，将```this._committing```置为true,理由是在源代码的251行```resetStoreVM```函数中判断严格模式的代码，如下：
  ```
  if (store.strict) {
    enableStrictMode(store)
  }
  ```
  * 当 vuex设置为严格模式， 执行enableStrictMode函数， 源码如下：
  ```
function enableStrictMode (store) {
    // $watch 函数来观察 state的变化
    store._vm.$watch(function () { return this._data.$$state }, () => {
    // tate变化时,调用 assert函数
    if (process.env.NODE_ENV !== 'production') {
    // 判断 store._committing
      assert(store._committing, `do not mutate vuex store state outside mutation handlers.`)
    }
    }, { deep: true, sync: true })
}
  ```
  * 当```store._committing```（this._committing）不为true，就会报出异常。
  
所以，当不是触发mutation来修改state， 就不会执行commit函数，也不会执行```_withcommit```函数，进而```this._committing```不会被修改成true,当执行 enableStrictMode 时,会执行 assert 函数，就会报出异常。

### 回归标题,action可以修改state吗？
可以，但是不提倡。  

综上所述，经测试得知可以修改并修改成功，但是严格模式下控制台会抛异常

### 结语：
我们开发要严格按照官方文档开发，避免不必要的错误产生。



