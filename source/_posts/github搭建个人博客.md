---
title: 结合 github 和 hexo 搭建个人博客
categoty: 关于编程
tag: 博客搭建
date: 2017/12/13
toc: true 
#  控制是否显示文章目录
description: 本文主要记录使用github和hexo搭建个人博客的一些步骤和难点，方便今后查阅。
---

+ 开始搭建个人博客之前，我们的计算机上需要已经安装了 node.js 、git和 hexo。

### 开始创建博客
+ 选择一个目录创建一个文件夹，用来存放所有blog东西
+ cd  到该文件夹下初始化命令  hexo init   会看到以下文件：
  - node_modules：是依赖包
  - public：存放的是生成的页面
  - scaffolds：命令生成文章等的模板
  - source：用命令创建的各种文章
  - themes：主题
  - _ config.yml：整个博客的配置
  - db.json：source解析所得到的
  - package.json：项目所需模块项目的配置信息
+ 在gitbash中，配置github账户信息（YourName和YourEail都替换成自己的）

```
  $git config --global user.name "YourName"
  $git config --global user.email "YourEmail"
```
+ 在 github 中新建一个仓库，名字格式： yourname.github.io
+ 生成本地 ssh 密钥，并添加到 github 上
  - 在 gitbash 中输入以下代码生成 ssh（邮箱写自己的邮箱）

  ```
    ssh-keygen -t rsa -C "youremail@example.com"
  ```
  - 找到本地秘钥的两种方式：
    1. 在用户/administrator/.ssh 目录下的  id_rsa.pub文件中
    2. 在博客目录下的 gitbash 中输入下面代码可以获得秘钥内容

  ```
    $ cd ~/.ssh
    $ cat id_rsa.pub
  ```
+ 在gitbash中验证是否成功添加密钥：

```
  ssh -t git@github.com
```
  - 成功提示信息：

  ```
    PTY allocation request failed on channel 0
  ```

+ 用编辑器打开你的blog项目，修改_config.yml文件的一些配置(冒号之后都有一个半角空格)：

```
deploy:
    type: git
    repo: https://github.com/YourgithubName/YourgithubName.github.io.git
    branch: master
```
+ 回到gitbash中，进入你的blog目录 安装 hexo-server 服务 并执行一些代码(hexo clean：清除生成的静态文件    hexo generate：生成静态文件)

```
  npm i hexo-server
  hexo clean   
  hexo generate  
  hexo server
```
  - 打开浏览器输入：http://localhost:4000 可以从本地看到hexo默认模板
+ 上传到github
  - 安装git提交服务

  ```
    npm install hexo-deployer-git --save
  ```

  - 执行下面命令

  ```
    hexo clean
    hexo generate    简写 hexo g
    hexo deploy        简写 hexo d
  ```

  - hexo generate 和 hexo deploy两个命令可以简写为：

  ```
    hexo g -d
  ```

  + 注意deploy的过程中要输入你的username及passward

  - 在浏览器中输入http://yourgithubname.github.io 就可以看到自己的个人博客了
  + 感觉gitbash中东西太多的时候可以输入clear命令清空。

### 个人博客的迁移
+ 具体的思路是：在博客页面代码master分支下新建立一个分支hexo，利用这个分支来管理自己的源文件。

#### 迁移前的准备：
+ 在github上新建一个hexo 分支，（搜索，显示没有，然后添加）
+ 本地 blog 代码中新建一个hexo分支

```
  git  branch  hexo
```
+ 同步hexo 分支和master分支内容（这一步也可能不需要）

```
  git  merge  master
```
+ 将hexo 分支push到github

```
  第一次push:  git  push  origin –u  hexo
  以后push :  git  push  origin  hexo  
```
+ 以后更新博客的步骤：
+ 思路：在hexo 分支上更新内容，保存，提交，推到远端，然后切换到主分支，将hexo 分支合并到主分支上，将主分支发布。

  - 在hexo 分支更新

  ```
    git  add  .
    git  commit  -m'提示信息'
    git  push origin   hexo

  ```
  - 切换到master分支

  ```
    git  checkout  master
  ```
  - 将hexo 分支合并到master分支

  ```
    git  merge  hexo
  ```
  - 将主分支分布

  ```
    hexo  clean
    hexo  g  -d
  ```

#### 在新的电脑上部署博客
+ 新的电脑上面需要重新安装 Git Bash 、Node.Js 和 hexo、重新设置账户名和邮箱、重新生成ssh密钥，并添加到github上（详情参照上面教程）

+ 在新的电脑上克隆github   hexo分支

```
  git clone -b hexo https://github.com/yourname/hexo-test.github.io.git
```
+ 安装依赖包

```
  npm  install
```
+ 因为不是新建博客，所以千万不能使用hexo init 命令

+ 查看所有分支,发现只有一个hexo 分支，没有master分支

```
  git branch –a
```
+ 新建master分支

```
  git branch master
```
+ 安装git提交服务

```
  npm install hexo-deployer-git - -save
```
+ 以后更新博客的步骤：
+ 在hexo 分支上更新内容，保存，提交，推到远端，然后切换到主分支，将hexo 分支合并到主分支上，将主分支发布。(操作命令不再赘述)
