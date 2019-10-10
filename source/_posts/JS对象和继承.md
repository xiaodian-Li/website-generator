---
title: JS对象和继承
date: 2019-10-10 14:49:05
tags:
---
## 对象创建的三种方式
#### 字面量创建方式
```
var person =｛
  name: 'Tom'　
｝
```
#### 系统内置构造函数方式
```
var person = new Object()
person.name = 'Tom'
```
<!--more-->

#### 自定义构造函数
```
function Person(name){
    this.name = name;
}
var person = new Person('Tom');
```

## 继承方式
#### for in 继承
```
function Person () {
  this.name = 'Tom'
  this.age = 25
}

function Son () {}
var p = new Person()
var s = new Son()
for (var k in p) {
  s[k] = p[k]
}
console.log(s.name) // Tom
console.log(s.age) // 25
```
#### 原型 + 构造函数的继承
```
function Person () {
  this.name = 'Tom'
  this.age = 25
}
function Son () {}
Son.prototype = new Person() // Son的原型指向Person的实例
var m = new Son() // 实例赋值给m

console.log(m.name) // Tom
console.log(m.age) // 25
```
#### Object.create经典继承
```
var person = {
  name: 'Tom',
  age: 25
}
var son  = Object.create(person)
console.log(son.name) // Tom
console.log(son.age) // 25

<!-- Object.create()是让一个对象的原型继承另外一个对象；所以虽然a.name和a.age是可以访问成功的，但实际上a本身并没有这些属性，而是a的原型上有这些属性。 -->
```
#### call, apply实现继承
* 构造函数的名字.call( 当前对象，属性，属性....) 解决了属性继承问题，但是不能继承父级的方法
```
function Person (name, age) {
  this.name = name
  this.age = age
}

function Student (name, age, score) {
  // Person.apply(this, [name, age]) // apply实现继承
  Person.call(this, name, age) // call实现继承
  this.score = score
}

var a = new Student('李四', '25', '100');
console.log(a.name) // 李四
console.log(a.age) // 25
console.log(a.score) // 100
```

相关文章： https://www.jianshu.com/p/b163e72aa8ae