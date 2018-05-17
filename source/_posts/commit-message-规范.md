---
title: commit message 规范
date: 2018-04-17 10:58:12
tags: [git]
categories: 前端知识
---
(这段时间做项目发现，多人合作时或者查看自己修改的以前版本，即使描述很清晰，
一天提交很多版本的情况下，也要逐一仔细查看变化，不是很直观)  
下面分享下这两天用的Commit message 的格式  
<!--more-->
### 1.对比  
before | after | after
---|---|---
![速运前端团队 > commit message > image2018-4-13 18:8:37.png](https://images.daojia.com/assets/other/images/1.png)   | ![速运前端团队 > commit message > image2018-4-13 18:8:37.png](https://images.daojia.com/assets/other/images/2.png)  | ![速运前端团队 > commit message > image2018-4-13 18:8:12.png](https://images.daojia.com/assets/other/images/3.png) 

### 2.前提：  
每次本地代码改动提交到远程，需要注明提交说明，否则不允许提交到远程
```
git commit -m "hello word" // -m: 指定hello word
```
提交多行信息：
```
git commit // 跳出文本编辑器，写多行信息
```
### 3.commit message 格式  
每次提交，包括三个部分： header, body, footer
```
<type>(<scope>): <subject> // 必须

				<body> // 可省略

				<footer> // 可省略
```
解释：

type: 提交类别（下面基本会覆盖提交代码所需，建议只出现下面7种类别，多了会更乱）

feat：新功能（feature）  
fix：修补bug  
docs：文档（documentation）  
style： 格式（不影响代码运行的变动）  
refactor：重构（即不是新增功能，也不是修改bug的代码变动）  
test：增加测试  
chore：构建过程或辅助工具的变动  
scope：影响范围（可不写）  
subject：对改变的正常描述，最好以动词开头语（尽量详细，必填）  
body：详细描述（个人认为没必要，可不写）  
footer：修改不兼容变动以及关闭   Issue时（个人认为没必要，可不写）  
### 4.撰写合格 Commit message 的工具----Commitizen
 
安装：
```
npm install -g commitizen
```
在项目目录里运行
```
commitizen init cz-conventional-changelog --save --save-exact
```
END： 以后凡是用git commit命令 就换成  git cz 

这样会自动提示以上几个类别

### 5.建议不必安装Commitizen工具，自己强制写几天就记住这七种类别了，安装校验反而积累
<br>

> 更多内容:   
https://lixiaoyu2017.github.io/  
> 参考文章:  
 http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html  
