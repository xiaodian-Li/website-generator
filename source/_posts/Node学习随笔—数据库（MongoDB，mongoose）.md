---
title: Node学习随笔—数据库（MongoDB，mongoose）
date: 2018-09-30 17:23:58
tags: [node, 数据库（MongoDB，mongoose）]
---
1.安装  
2.MongoDB组成  
数据库里存放集合，集合里存放文档  

数据库： 一个仓库，可以存放集合<br><!--more-->

集合： 类似于数组， 在集合中存放文档  

文档： 文档数据库的最小单位，我们存储和操作的内容都是文档  

3.MongoDB的增删改查（注意各个方法的参数）  
http://www.mongodb.org.cn/  

https://docs.mongodb.com/manual/crud/  
```
find----查找

// 查询数据库colleges集合中的name为html5的文档

db.colleges.find({name: "html5"});



update----添加/替换

// 数据库colleges集合中的name为html5的文档，添加intro属性，值为"我正在学习数据库"

db.colleges.update({name: "html5"}, {$set: {intro: "我正在学习数据库"}});
// 使用{name: "大数据"} 替换 name为"K12"的文档
db.colleges.update({name: "大数据"}, {$set: {name: "K12"}});  // $unset用作删除
注意：文档插入文档用$set一步步插入，取得时候用对象.属性取出即可
更新替换也可用<数组更新操作符>
remove/drop------删除
```
4.批量数据的删除，修改和替换  
```
// 向集合demos集合中插入10000个文档（insert可以实现，但是每次都做重复插入性能不好）

var arr = []

for (var i=0, i<10000, i++) {

   arr.push ({count: i})

}

db.demos.insert(arr)



// 查找集合中大于或者小于多少的-------用比较查询运算符

// 查询demos中couter小于666的文档

db.demos.find({cputer: {$lt: 666}})



// 查询demos中couter大于66小于666的文档

db.demos.find({cputer: {$lt: 66, $lt: 666}})
// 查询demos集合中11条到20条数据，limit 10为10条数据

db.demos.find().skip(10).limit(10) 
```
5.多集合操作
```
// 创建company数据库并导入it666, section---可视化直接导入

db.it666.find()

db.section.find()



// 查询html5学院所有的老师， 因为html5对应的num是唯一的 所以：

var num = db.it666.findOne({"cname": "html5学院"}).num

db.section.find({num: num})
```
6.集合间对应关系
```
一对一: eg  身份证和人

一对多/多对一：eg 父母和孩子， 找唯一对应关系。

多对多： eg  学生和老师
```

7.排序和索引
```
排序：查询时默认为升序，按照id的值， 也可利用solt()指定,需要传一个对象，1升序，-1降序

db.section.find().sort({wage: 1})

limit限制查找个数

skip限制跳转个数

索引：映射（适用于只需要部分文档数据，在查询时第二个参数设置结果投影）
db.section.find({},{name: 1, wege: 0, bonus:1}) // 1显示 0不显示
```
8.mongoose
1.mongoose是让我们可以通过Node来操作MongoDB的模块

2.安装： npm i mongoose --save

相关上手文档如下：

https://mongoosejs.com/docs/index.html

![](http://images.daojia.com/assets/other/images/gitimg/node6.png)

3.常用API中model方法 


注意：修改方法要加$set


4.删除remove，delect都可（在实际开发中用的最多的是remove）


