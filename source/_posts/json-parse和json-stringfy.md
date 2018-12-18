---
title: json.parse和json.stringfy
date: 2018-12-18 15:08:57
tags: [js]
---
1.parse用于从一个字符串中解析出json对象,如  
var str = '{"name":"huangxiaojian","age":"23"}'  

结果：<br><!--more-->
JSON.parse(str)

Object:
```
    {
        age: "23"
        name: "huangxiaojian"
        __proto__: Object
    }
```

注意：单引号写在{}外，每个属性名都必须用双引号，否则会抛出异常。


2.stringify()用于从一个对象解析出字符串，如    

var a = {a:1,b:2}  

结果：  
JSON.stringify(a)
```
"{"a":1,"b":2}"
```