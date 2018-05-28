---
title: 几张图让你彻底弄懂git工作流(三) ——git深入
date: 2018-05-28 15:35:05
tags: [git]
---
前两篇文章分别说了[git简史与git基础](https://xiaodian-li.github.io/2018/05/18/%E5%87%A0%E5%BC%A0%E5%9B%BE%E8%AE%A9%E4%BD%A0%E5%BD%BB%E5%BA%95%E5%BC%84%E6%87%82git%E5%B7%A5%E4%BD%9C%E6%B5%81-%E4%B8%80-%E2%80%94%E2%80%94git%E7%AE%80%E5%8F%B2%E4%B8%8Egit%E5%9F%BA%E7%A1%80.md/)以及[git分支](https://xiaodian-li.github.io/2018/05/28/%E5%87%A0%E5%BC%A0%E5%9B%BE%E8%AE%A9%E4%BD%A0%E5%BD%BB%E5%BA%95%E5%BC%84%E6%87%82git%E5%B7%A5%E4%BD%9C%E6%B5%81-%E4%BA%8C-%E2%80%94%E2%80%94git%E5%88%86%E6%94%AF/)，那么这篇文章开始简单描述一下git深入
# Git深入
在 Git 中提交时，会保存一个提交（commit）对象，该对象包含一个指向暂存内容快照的指针，包含本次提交的作者等相关附属信息，包含零个或多个指向该提交对象的父对象指针：首次提交是没有直接祖先的，普通提交有一个祖先，由两个或多个分支合并产生的提交则有多个祖先  <!--more-->
<br>

* 存储快照——仓库中的各个对象保存的数据和相互关系如下

单个提交对象在仓库中的数据结构 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git22.png) | git commit 提交对象前，git会先计算每一个子目录的校验和，然后在git仓库中将目录保存为树对象，所以在创建提交对象不担包含提交信息还包含指向树（项目根目录）的指针，在将来需要的时候，重现此次快照的内容
如上五个对象：三个文件快照内容blob对象，一个目录树内容及其中各个文件对应 blob 对象索引的 tree 对象，一个包含指向 tree 对象（根目录）的索引和其他提交信息元数据的 commit 对象
<br>

* git存储解构示意图


图示 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git231.png)  | 有三个提交的Git仓库可简化为左图
![](http://images.daojia.com/assets/other/images/gitimg/git232.png) | 上面只有提交的图补上分支后
![](http://images.daojia.com/assets/other/images/gitimg/git23.png) | 上面的图补上HEAD后,如左图所示
<br>

* .git目录介绍

Git仓库下有一个.git目录，里面存储了git全部的秘密，一般包括下面的内容：  
1. config  
 config是仓库的配置文件，一个典型的配置文件如下，我们创建的远端，分支都在配置文件里有表现； fetch操作的行为也是在这里配置的
1. index
1. HEAD
HEAD文件存储的是当前所在的位置，其内容可以使分支名字，40位commit ID
1. hooks/
1. logs/
1. refs/  
 refs目录存储都是引用文件，如本地分支，远端分支，标签等  
refs/heads/xxx 本地分支  
refs/remotes/origin/xxx 远端分支  
refs/tags/xxx 本地tag  
1. objects/  
git通过一种算法可以得到任意文件的指纹(40位16进制数字)，然后通过文件指纹存取数据，存取的数据都位于objects目录
<br>
> 文章出处：起底Git & Pro Git