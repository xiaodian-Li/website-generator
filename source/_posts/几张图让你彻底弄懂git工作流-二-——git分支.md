---
title: 几张图让你彻底弄懂git工作流(二) ——git分支
date: 2018-05-28 11:40:42
tags: [git]
---
上篇文章已经说了Git简史以及Git基础，那么这篇文章简单总结下Git分支
# Git分支
为了理解 Git 分支的实现方式,我们需要回顾一下,
Git保存的不是文件差异或者变化量，而只是一系列文件快照. <br><!--more-->

* Git分支  

分支其实就是从某个提交对象往回看的历史 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git4.png) | Git中的分支，本质上就是个指向master对象的可变指针，master为默认分支，每次提交都会向前移动


多个分支指向提交数据的历史 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git5.png) | Git创建一个新分支指针从而创建分支，创建testing命令git branch testing


HEAD 指向当前所在的分支 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git6.png) | Git因为保存一个名为HEAD的指针，它指向正在工作中本地分支指针<br>git branch仅是创建新分支，但不会自动切换分支中去（如图还在master上）


HEAD 在你转换分支时指向新的分支 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git7.png) | 运行git checkout testingHEAD就指向testing分支了

每次提交后 HEAD 随着分支一起向前移动 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git8.png) | 左图是又提交一次的结果，每次提交后HEAD随着分支一起向前移动<br>但master仍指向原来git checkout时所在的commit对象。再次执行git checkout masterHEAD才会指向master
<br>

* Git—merge

分支的合并 — merge #1 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git10.png)  | **1. #53是第一滴修补问题的分支**<br>git chackout -b iss53 === git branch iss53+git checkout iss53<br>**2.假如接到紧急任务**，这时候就不必花费大力气来复原这些修改，执行git checkout master创建紧急修补分支git checkout -b hotfix<br>**3.hotfix分支**是从master分支所在点分化出来的
![](http://images.daojia.com/assets/other/images/gitimg/git11.png) | **1.测试成功后**回到master把它合并起来，然后发布服务器，命令为git checkout master git merge hotfix 合并会出现“Fast forward”的提示<br>**2.因为**是master并入hotfix的直接上游，只需master指针右移动（顺着走）称为快进<br>**3.合并之后**，master 分支和 hotfix 分支指向同一位置


分支的合并 — merge #2 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git12.png) | 1.现在回来处理iss53，完成后合并回master,不同于hotfix,开发历史从早的地方开始分叉的<br>2.master->c4，git额外处理为找到共同祖先C2简单三方合并
![](http://images.daojia.com/assets/other/images/gitimg/git13.png) | 三方合并后的结果重新快照，并自动创建指向它的提交对象C6,可以看到C6有两个祖先<br>  (git自动创建了一个包含了合并结果的提交对象，自己裁决哪个共同祖先才是最佳合并基础，这和 CVS及Subversion（1.5 以后的版本不同)
<br>

* Git—rebase

分支的合并 — rebase #1 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git14.png) | 把一个分支中的修改整合到另一个分支的办法有两种：merge 和 rebase（衍合）<br>如左图：分叉到两个不同分支，又各自提交了更新
![](http://images.daojia.com/assets/other/images/gitimg/git141.png) | 除了merge两个分支最新的公共祖先三方合并<br>另外就是C3的变化补丁在C4中重新打一遍->衍合<br>有了衍合可以把分支中提交的变化移到另一个分支重放一遍<br>（原理：回到共同祖先，根据当前分支（ex··）提交的对象C3,生成补丁然后以master最后提交的C4为新的出发点，逐个应用之前准备好的补丁文件，最后会生成一个新的合并提交对象（C3'），master成直接下游）
![](http://images.daojia.com/assets/other/images/gitimg/git15.png) | 回到master进行快进合并


分支的合并 — rebase #2 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git17.png)  | 从一个特性分支里再分出一个特性分支的历史<br>服务器端代码添加功能创建server提C3C4->从C3增加client分支并提C8C9->回server提C10
![](http://images.daojia.com/assets/other/images/gitimg/git18.png) | 将特性分支上的另一个特性分支衍合到其他分支<br>一次软件发布中，我们决定先把客户端的修改并到主线中，而暂缓并入服务端软件的修改<br>git rebase --onto master server client<br>取出 client 分支，找出 client 分支和 server 分支的共同祖先之后的变化，然后把它们在 master 上重演一遍
![](http://images.daojia.com/assets/other/images/gitimg/git16.png) | 快进 master 分支，使之包含 client 分支的变化<br>git checkout master<br>git merge client
![](http://images.daojia.com/assets/other/images/gitimg/git20.png) | 在 master 分支上衍合 server 分支<br>git rebase [主分支] [特性分支] 命令会先取出特性分支 server，然后在主分支 master 上重演<br>git rebase master server
![](http://images.daojia.com/assets/other/images/gitimg/git201.png) | 最终的提交历史<br>快进主干分支 master<br>git checkout master && git merge server 
现在 client 和 server 分支的变化都已经集成到主干分支来了，可以删掉它们了  
git branch -d client  
git branch -d server
<br>

* Git—rebase风险

分支的合并 — rebase的风险 | 文字描述
---|---
把衍合当成一种在推送之前清理提交历史的手段，而且仅仅衍合那些尚未公开的提交对象，就没问题。 | 如果衍合那些已经公开的提交对象，并且已经有人基于这些提交对象开展了后续开发工作的话，就会出现叫人沮丧的麻烦

<br>
* Git分支—远端同步

git分支 — 和远端同步 | 文字描述
---|---
![](http://images.daojia.com/assets/other/images/gitimg/git21.png) | 如左图箭头中命名所示即可与远端同步  

<br>
更多内容请查看[《几张图让你彻底弄懂git工作流(三)——git深入》](https://xiaodian-li.github.io/2018/05/28/%E5%87%A0%E5%BC%A0%E5%9B%BE%E8%AE%A9%E4%BD%A0%E5%BD%BB%E5%BA%95%E5%BC%84%E6%87%82git%E5%B7%A5%E4%BD%9C%E6%B5%81-%E4%B8%89-%E2%80%94%E2%80%94git%E6%B7%B1%E5%85%A5/)😊 