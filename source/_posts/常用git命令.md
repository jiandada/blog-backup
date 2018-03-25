---
title: 常用git命令
category: 关于编程
tag: git
date: 2018/3/25
toc: true
description: git常用命令总结，以便今后查阅。
---

### git简介
+ Git有三个工作状态，分别是已修改（modified）、已暂存（staged） 和已提交（committed）。
+ 由此引入 Git 项目的三个工作区域的概念：Git 仓库、工作目录以及暂存区域。
- Git仓库目录是Git用来保存项目的元数据和对象数据库的地方。 这是Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。
- 工作目录是对项目的某个版本独立提取出来的内容。这些从Git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。
- 暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在Git仓库目录中。有时候也被称作“索引”（Index），不过一般说法还是叫暂存区域。

### 基本的git工作流程
+ 在工作目录中修改文件。
+ 暂存文件，将文件的快照放入暂存区域。
+ 提交文件，找到暂存区域的文件，将快照永久性存储到Git仓库目录。

### git基础

#### git配置用户
+ git config --global user.name "自已的名字"
+ git config --global user.email "自已的邮箱地址"
+ --global 配置当前用户所有仓库
+ --system 配置当前计算机上所有用户的所有仓库
+ 注：配置用户只需要执行1次，可以重复使用。

#### 初始化仓库
+ 我们如果想要利用git进行版本控制，需要将现有项目初始化为一个仓库。
- git init
+ git init只是创建了一个名为.git的隐藏目录，这个目录就是存储我们历史版本的仓库

#### 查看文件状态
+ 通过git status可以检测当前仓库文件的状态

#### 添加文件到暂存区
+ git add 文件名/ 文件路径 “*”或-A代表所有
+ 一般用  git add  .    添加所有
+ 放到暂存区的文件被标记成了绿色，等待提交。

#### 提交文件
+ git commit -m '备注信息'
+ 将暂存区被标记成绿色的文件，全部提交到本地仓库存储。

#### 查看提交历史
+ git log查看提交的历史
+ 我们可以查看到一次次提交记录，代表一次提交的唯一ID一般称为SHA值。

#### 恢复上一次提交的状态
+ 通过SHA值可以回到之前某一次的提交（时光倒流）
+ git reset --hard xxxx(哈希值的前八位即可)

### Git分支

#### 创建分支
+ git branch dev
- 新建的子分支会继承父分支的所有提交历史

#### 切换分支
+ git checkout dev

#### 合并分支
+ git merge dev
- 在主分支上执行此命令，即可将dev分支合并到主分支上
+ 分支冲突的话需要手动合并

#### 删除分支
+ git branch -d dev

### 本地项目push到github的相关操作
+ git remote add origin	git@xxx.git  添加远端仓库（第一次添加）
+ git push –u origin master	 将本地项目以流的形式push到远端的master(主分支)上。
+ git pull origin master 将远端的更新获取到本地
+ git clone xxx(github上的仓库地址)   克隆

