---
title: 源码系列：Vuex为什么不允许在action中修改state?
date: 2019-12-10 19:05:26
tags: [vue, vuex]
---

### 背景
在最近的一次需求开发过程中，有再次使用到Vuex，在状态更新这一方面，我始终遵循着官方的“叮嘱”，谨记“一定不要在action中修改state，而是要在mutation中修改”；于是我不禁产生了一个疑问：Vuex为什么要给出这个限制，它是基于什么原因呢？带着这个疑问我查看Vuex的源码，下面请大家跟着我的脚步，来一起揭开这个问题的面纱
<!--more-->

### 一起阅读源码吧~

1.首先我们可以在src/store.js这个文件的Store类中找到下面这段代码
```javascript
// ...
this.dispatch = function boundDispatch (type, payload) {
      return dispatch.call(store, type, payload)
    }
    this.commit = function boundCommit (type, payload, options) {
      return commit.call(store, type, payload, options)
    }
// ...
```

上面是Vuex两个最核心的API：dispatch & commit，它们是分别用来提交action和mutation的
那么既然我们今天的目的是为了“了解为什么不能在action中修改state”，所以我们就先看看mutation是怎样修改state的，然而mutation是通过commit提交的，所以我们先看一下commit的内部实现

#### commit&mutation
2.commit方法的核心代码大致如下：
```javascript
commit (_type, _payload, _options) {
    // ...
    this._withCommit(() => {
      entry.forEach(function commitIterator (handler) {
        handler(payload)
      })
    })
    // ...
}
```

不难看出，Vuex在commit（提交）某种类型的mutation时，会先用_withCommit包裹一下这些mutation，即作为参数传入_withCommit；那么我们来看看_withCommit的内部实现（ps：这里之所以说”某种类型的mutation“，是因为Vuex的确支持声明多个同名的mutation，不过前提是它们在不同的namespace下；action同理）

3._withCommit方法的代码如下：
```javascript
_withCommit (fn) {
    const committing = this._committing
    this._committing = true
    fn()
    this._committing = committing
  }
```

是的，你没有看错，它真的只有4行代码；这里我们注意到有一个标志位_committing，在执行fn前，这个标志位会被置为true，这个点我们先记下，一会儿会用到

4.接下来，我要为大家要介绍的是resetStoreVM这个函数，它的作用是初始化store，它首次被执行是在Store的构造函数中
```javascript
function resetStoreVM (store, state, hot) {
  // ...
  if (store.strict) {
    enableStrictMode(store)
  }
// ...
}
```

在这里有一处需要我们注意：resetStoreVM对strict（是否启用严格模式）做了判断，这里假设我们启用严格模式，那么就会执行enableStrictMode这个函数，下面继续来看看它的内部实现

```javascript
function enableStrictMode (store) {
  store._vm.$watch(function () { return this._data.$$state }, () => {
    if (process.env.NODE_ENV !== 'production') {
      assert(store._committing, `do not mutate vuex store state outside mutation handlers.`)
    }
  }, { deep: true, sync: true })
}
```

这里对Vue组件实例的state做了监听，一旦监听到变化，就会执行asset（断言），它断言的恰巧就是刚才我让大家记住的那个_committing标志位，那么我们再来看看这个asset做了些什么

5.asset方法在src/util.js这个文件中
```javascript
export function assert (condition, msg) {
  if (!condition) throw new Error(`[vuex] ${msg}`)
}
```

这个方法很简单，就是判断第一个参数是否为truly值，如果不为真，就抛出一个异常  

到此，我们已简单地了解了commit和mutation的逻辑，下面再来看看dispatch和action

#### dispatch&action
6.dispatch代码大致如下：
```javascript
dispatch (_type, _payload) {
    const {
      type,
      payload
    } = unifyObjectStyle(_type, _payload)

    const action = { type, payload }
    const entry = this._actions[type]

  // ...
    const result = entry.length > 1
      ? Promise.all(entry.map(handler => handler(payload)))
      : entry[0](payload)
  // ...
  }
```

这里我们注意到，当某种类型的action只有一个声明时，action的回调会被当作普通函数执行，而当如果有多个声明时，它们是被视为Promise实例，并且用Promise.all执行，总所周知，Promise.all在执行Promise时是不保证顺序的，也就是说，假如有3个Promise实例：P1、P2、P3，它们3个之中不一定哪个先有返回结果，那么我们仔细思考一下：如果同时在多个action中修改了同一个state，那会有什么样的结果？

其实很简单，我们在多个action中修改同一个state，因为很有可能每个action赋给state的新值都有所不同，并且不能保证最后一个有返回结果action是哪一个action，所以最后赋予state的值可能是错误的

那么Vuex为什么要使用Promise.all执行action呢？其实也是出于性能考虑，这样我们就可以最大限度进行异步操作并发

眼尖的同学可能已经发现在dispatch中并没有看到_committing的身影，就是Vuex对action修改state的限制：当action想要修改state时，因为_committing没有事先被置为true，而导致asset阶段无法通过

但这个限制只限于开发阶段，因为在enableStrictMode函数中，Webpack加入了对环境的判断，如果不是生产环境（也就是开发环境）才会输出asset（断言）这行代码

```javascript
function enableStrictMode (store) {
  store._vm.$watch(function () { return this._data.$$state }, () => {
    if (process.env.NODE_ENV !== 'production') {
      assert(store._committing, `do not mutate vuex store state outside mutation handlers.`)
    }
  }, { deep: true, sync: true })
}
```

那么也就是说如果你强行在生产环境中用action修改state，Vuex也不会阻止你，它可能仅仅是给你一个警告；而且按道理来说，如果我们能够保证同一类型的action只有一个声明，那么无论是使用action还是mutation来修改state结果都是一样的，因为Vuex针对这种情况，没有使用Promise.all执行action，所以也就不会存在返回结果先后问题

```javascript
dispatch (_type, _payload) {
    // ...
    const result = entry.length > 1
      ? Promise.all(entry.map(handler => handler(payload)))
      : entry[0](payload)
    // ...
  }
```

但是凡是靠人遵守的约定都是不靠谱的，所以我们在平时使用Vuex时，最好还是遵守官方的约束，否则线上代码有可能出现bug，这不是我们所期望的

### 结束语
Vuex这一限制其实也是出于代码设计考虑，action和mutation各司其事，本质上也是遵守了“单一职责”原则。以上就是我对“Vuex为什么不允许在action中修改状态“这个问题的分析，希望对大家有所帮助，也欢迎指正





