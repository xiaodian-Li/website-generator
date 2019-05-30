---
title: ES6新特性
date: 2019-05-30 14:17:11
tags: [js, ES6]
---
#### 本文列举一些我们开发常用的ES6新特性， 如下：
![image](https://static.daojia.com/assets/project/tosimple-pic/es6新特性_1559185110760.png)
<!--more-->
#### 1.块级作用域变量let，const
* let, const不会出现变量提升
* let 和 const 不允许重复声明(会抛出错误)
* let 和 const 定义的变量在定义语句之前，如果使用会抛出错误(形成了暂时性死区)
* let 声明变量， const声明常量

#### 2.新增基本数据类型Symbol
ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值  
保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突

#### 3.结构赋值
```
var [a,b,c]=[11,22,33]
console.log(a,b,c)//11 22 33

var {name,age}={name:"张三",age:"20"}
console.log(name,age)//张三 20

```

#### 4.给形参设置默认值&箭头函数
给形参设置默认值
```
function defaultValue (a=10, b=20) {
    console.log(a, b)  // 10,20
}
defaultValue(100, 200) // 100, 200
defaultValue(11) // 11, 20
```
箭头函数
```
//普通函数
var fun1 = function(a){
    console.log(a);
}
//箭头函数
var fun1 = (a)=>{console.log(a);}
fun1(3);
```

#### 5.对象或者数组的展开符 ...
```
var arr = [1,2,3];
console.log(...arr)// 1 2 3
```

#### 6.String的include方法
includes("元素"); 用于判断字符串中是否包含某个字符
存在返回true 不存在返回false

#### 7.Array新增API：isArray/from/of 和新增方法：entries()/kes()/values()等
* isArray判断是否是数组
* Array.from() 方法从一个类似数组或可迭代对象中创建一个新的数组实例。
```
var a = {
  0:'0',
  1:'1',
  2:'2',
  length:3
}

a = Array.from(a)

console.log(a) // ["000", "111", "222"]
```
* Array.of() 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。
```
console.log(Array.of(1,2,3,{}, true)) //[1,2,3,{},true]
```
* Array.prototype.entries  
entries()返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对。
* Array.prototype.keys  
keys() 方法返回一个包含数组中每个索引键的Array Iterator对象。
* Array.prototype.values  
values() 方法返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值

#### 8.增加class语法糖
```
class 类名{
    constructor(){} // 构造函数
    run(){}// 函数属性
    dark(){}// 函数属性
}
```
#### 9.新增模块化（import/export）
export导出变量，模块，函数等
```
export function sum(num1,num2){
     return num1+num2;
}
等价于
function sun (num1,num2){
     return num1+num2;
}
export sum;
```
import导入写法
```
import {identifer1,indentifer2}  from "./example.js"  // import {标识符1，标识符2} from "本地模块路径"
```

#### 10.新增Map，Set数据结构
set（）没有重复的有序列表集合
* set包含的方法
add()、has()、delete()、clear()等   

Map() 用来存放键值对的集合 key/value

* get(key)根据key值取得value
```
var map = new Map();
map.set("name","张三");
map.set("age",20);
console.log(map)//Map {"name" => "张三", "age" => 20}
```
* has() 判断是否存在某个键值对
* clear() 清空集合

#### 11.模板字符串
```
语法:
tag `string text ${expression} string text`
```
#### 12.for...of 和 for...in
for...of 具有 iterator 接口，就可以用for...of循环遍历属性值，可终止  
使用的范围包括数组、Set 和 Map 结构、某些类似数组的对象、Generator 对象，以及字符串

for...in 遍历对象自身的和继承的可枚举的属性, 不能直接获取属性值。可以中断循环

