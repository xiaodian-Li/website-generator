---
title: beta——js通用工具库
date: 2018-05-30 21:02:33
tags: [js]
---
背景：针对业务需要，对js常用方法进行整合，提升开发效率    
github地址：https://github.com/xiaodian-Li/js-util
# 相关API
大致分为几类，详细api以及用法参考docx/api.md  <br><!--more-->

## 1.cookie
##### getCookie(name)根据 name 获取对应的 cookie 值。
##### hasCookie(name)查询名为 name 的 cookie 是否存在。
##### removeCookie(name, path, domain)移除名为 name 的 cookie。
##### setCookie(name, val, opts)设置 cookie。
##### removeCookie(name, path, domain)移除名为 name 的 cookie。
##### removeCookie(name, path, domain)移除名为 name 的 cookie。
##### removeCookie(name, path, domain)移除名为 name 的 cookie。
##### removeCookie(name, path, domain)移除名为 name 的 cookie。


## 2.storage
##### getStorage(key = '', type = 'local')根据散列和存储的key, 返回存储的 value
##### setStorage(key = '', val = '', type = 'local')修改或添加键值(key-value)对数据到应用数据存储中
##### removeStorage(key = '', type = 'local')通过key值删除键值对存储的数据
##### clearStorage(type = 'local')清除应用所有的键值对存储数据


## 3.url(获取与url相关的参数等)
##### getQueryParam(name, url)返回指定查询字符串参数的值（如果在当前页面 URL 中或在提供的字符串中找到）
##### getParams(str)返回一个名为str的参数
##### getQueryString (value)获取url上的文本


## 4.validator(常用验证)
##### bPhone(val)手机号码校验
##### bTel(val)座机校验
##### bID(val)简单校验，只校验位数
##### bIP(val)Func: 验证IP ，规则：（1~255）.（0~255）.（0~255）.（0~255）
##### bMail(val)邮箱校验
##### bIdCard (str)身份证验证，30个字符
##### bName (str, min, max)验证姓名，只支持20个汉字
##### bCarNum (str)验证车牌号
##### bPwd (str)验证密码 6-14位字符


## 5.platform(判断终端信息)
##### _getUA()判断浏览器类型
##### biOS()判断是否是ios设备
##### bAndroid()判断是否是安卓设备
##### bMobile()判断是哪个移动设备（返回android|webos|iphone|ipad|ipad）
##### bPC()判断是否是PC端（返回不是移动的设备）
##### bWechat()判断是否是微信端
##### bSuyunDriver()返回速运司机端
##### bSuyunUser()返回速运用户端
##### bSuyunUp()返回速运优配


## 6.formateTime(时间戳转化)
##### getYMD (str, slice = '-', err = '')将字符串时间转为时间戳 yyyy-mm-dd
##### getSeparator (stamp, slice = '-')将时间戳（Date对象）转化为字符串时间，第二个参数为分隔符，默认为-
##### getChangeStr (str, value, slice = '-')依赖于separator，运算字符串时间，value为天数，可以为为负数
##### getTMin (date, slice = ':', err = '暂无')获取时间xx:xx
##### getDur (sDate, eDate, cb = this.getTime)获取时间差值
##### getRemoveSec (str, slice = '-', err = '暂无')将字符串时间转为时间戳 yyyy-mm-dd hh:mm
##### getStampMore ()将字符串时间转为时间戳 yyyy-mm-dd hh:mm：ss
##### bLeapYear(year)判断是否为闰年



## 7.commonData(通用数据类型判断)
##### bUndefined (tmp)判断undefined,
##### bNull (tmp)判断null
##### bNaN (tmp)判断NAN
##### bNumber(val)判断数据类型为数值型number
##### bBooleanType(val)判断数据类型为布尔型（boolean）
##### bStringType(val)判断数据类型为字符串(String)
##### bObject(obj)判断是对象 
##### bPlainObject(obj)判断是否是Object
##### bEmptyObject(obj)判断是否是空对象
##### bArray(arr)判断判断arr是否是Array
##### bArrayLike(obj)判断判断obj是否是类数组
##### bFunction(fn)判断fn是否是Function
##### bWindow(obj)判断是否是Window 
##### bDocument(obj)判断是否是文档类型
##### getNodeName(elem, name)获取元素节点名称
##### getEach(obj, fn, context)遍利节点
##### getTrim(text)清除字符串空格
### 一.介绍大致目录
```
until                # 通用方法库
├── dist             # 编译后生成
├── docx             # 方法用法说明，更新日志说明
├── node_moules      # 打项目依赖
├── src              # 项目资源文件，代码出处
├── test             # 项目测试目录
├── 其他              # 项目，脚手架所需的基本配置

```
### 二.对于开发者
——2.1 开发+单测(Chai.js断言库中expect && 测试框架 Mocha对js进行单元测试)+发布  

describe块称为"测试套件"（test suite），表示一组相关的测试  
it块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。
——2.2 大致开发规范
### 三.发布版本说明
一般是从1.0.0开始
A.B.C----A表示大版本号，一般当软件整体重写，或出现不向后兼容的改变时，B功能更新，出现新功能，C小修改，如修复bug

### 四.对于使用者
——4.1 安装
——4.2 使用
——4.3 相关api

### 五.文档
相关文档除在readme中，还有docx文件里

### 六.Todo List
——6.1 在第一版中自己的方法中并没有用到方法，下一步需要进行整合（关联也是测试一部分）  
——6.2 方法可能不是太全，大家有什么方法类可以补充的，或者经常使用的方法需要补充  
——6.3 可以提给我or自己拉分支修改    
——6.4 单测可以更全面的覆盖  
 

