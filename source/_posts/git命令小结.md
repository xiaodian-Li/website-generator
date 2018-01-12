---
title: git命令总结
date: 2017-11-09 10:58:12
tags: [git脚本命令,git多人合作]
categories: 前端知识
---

(以下是入职以来，经常用到的一些命令，可以说是频繁，以此总结希望大家一起进步，在总结中收获成长)
##### 远程有仓库，怎样才能拉下代码至本地 （相当于开始的初始化）
这里以远程B仓库为例
* git clone B test
或者 git remote add origin B test  //把仓库克隆到本地并命名一个项目名称test
* git init   //在本地初始化创建仓库<br>
<!--more-->
* git branch master    //创建主支
* git branch dev //本地创建dev分支
* git checkout dev  //切换到dev分支
* git branch -b dev-1 //基于dev分支创建dev-1分支
* git checkout -b dev-1 //切换到dev-1分支并在其上操作

##### 本地修改代码后，怎样使用git命令提交到远程仓库呢？
* git status   //看本地修改状态
* git diff  ||  git diff (src)   //查看执行 git status 的结果的详细信息
* git rm <file>   //删除文件
* git add .（所有改变提交） //把改变添加到本地仓库
* git commit -m "提交信息   //提交到本地仓库
* git pull origin 远程分支名称   //先把远程分支拉取下来
* git push origin 自己的分支  //再把本地修改提交到远程

##### 关于分支
* git branch //查看分支
* git branch -d <name> //删除分支
* git merge <name> //合并dev分支到当前分支

##### 解决冲突，假定和A合作
* git reset --hard (跟A不一样，用A的)
* git status
* git stash (把自己本地的修改先暂存起来，避免冲突，再去拉A代码)
* git pull origin 分支名 (拉下来A的代码)
* git stash pop (把自己的代码释放)
* git log --pretty=oneline<br>//关于版本回退<br>//从最近到最远的提交日志 其中--pretty=oneline 目的为减少信息显示
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL  //commit id + commit Msg
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
* git reset --hard HEAD^ ||  git reset —hard HEAD~1 <br> //回退到 上一个版本 GPL -> add distributed<br>
注意：但是git log信息时，已经没有了 GPL的相关信息了
* 再回到最新版本：
$ git reflog   //命令历史可以得到 commit id<br>
$ git reset --hard 3628164 //回到 commit id  版本
* 把远程主机更新版本重新拉取回本地<br>
git fetch
##### 如何打tag
1.git tag -a 版本 -m "备注信息"<br>
2.git push origin 版本 || git push origin --tags   // 把tag上传到远程<br>
3.git show 版本 查看标签版本信息<br>
4.git tag -d 版本  // 删除标签<br>
5.git tag  // 查看当前分支下的标签

###### 参考文章<br>
1.https://git-scm.com/book/zh/v2<br>
2.http://www.bootcss.com/p/git-guide/<br>
3.https://segmentfault.com/a/1190000009565961本