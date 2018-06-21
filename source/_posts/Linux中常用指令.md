---
title: Linux中常用指令
date: 2018-06-20 16:37:24
tags: [Linux]
---
自我认为，命令行虽然不够直观，但是能沿用至今，好处不言而喻，其中本人感触最深的就是快，方便，能用命令行解决的，尽量别手动敲  <br><!--more-->
### 基本命令

命令 | 简介 | 示例
---|---|---|
pwd | 查看当前工作目录 | pwd
ls | 列出当前目录中的子目录及文件 | ls
cd | 切换转到指定路径 | cd /folder
mkdir | 创建新的目录 | mkdir 123 /demo 权限为123的demo文件夹
touch | 创建新文件 | touch xiaodian.text
rm | 删除文件/文件夹 | rm -i file // 删除文件file，在删除之前会询问是否进行该操作<br> rm -rf dir // 删除文件夹
file | 查看文件类型 | file a.js
cp | 复制文件/目录 | cp a.js b.js
mv | 移动文件/目录 | mv a.js b.js
which | 查看可执行文件的位置 | which 可执行文件名称 
ln | 创建文件/目录的链接 | ln node-v6.2 node 
find | 查找文件或目录 | /

### 内容查看命令

命令 | 简介 | 示例
---|---|---|
vi | 进入某个文件 | vi aaa.txt
vi->i | 进入文件后，编辑模式 | /
vi->ESC | 进入文件后，回到一般模式 | /
vi->:wq | 进入文件后，退出保存 | /
cat | 查看显示文件内容 |  cat a.js
more/less | 分页查看文件内容 | /
head/tail | 查看文件开头/末尾的部分内容	 | /
grep | 检索过滤文件内容 | grep ‘vue’
<br>
（未完待续）