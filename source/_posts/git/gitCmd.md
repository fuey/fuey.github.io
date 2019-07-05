title: git常用命令
tags: [git]
keyword: git,git常用命令
categories: git
type: "wiki"

---
# git常用命令

> 好不容易搭好的博客，前几次改了几个文件，差点GG，所以为了以防不测，故上传github，备份之!<!-- more -->

* `touch README.md` 创建并添加一个名字为readme.md的文件
* `git init` 初始化git仓库
* `git add README.MD` 添加一个文件到本地仓库，用于之后的提交(只有在本地代码库里面的代码才能够提交到git的远程仓库上去)
* `git add .` 添加当前路径下的所有文件到本地仓库(注意那个.与add中间有一个空格)
* `git commit -m "notes"` 为本次提交加注释(即本次提交的代码主要简介)
* `git remote add origin https://github.com/***/***.git` 创建远程仓库，并为仓库命名,**origin**为仓库的别名(origin则设为默认主机)，用于将来引用,此处的**url**为git上事先创建好的url地址
* `git push -u origin master` 本地的master分支推送到origin主机的master分支
* `git pull --rebase origin master` 代码合并
* `git config --global --unset http.proxy` （出现这个错误时：`fatal: unable to access 'https://github.com/fuey/blog-code-backups.git/': Couldn't resolve host 'github.com'`，然后再提交就行了）

## 提交分支一般步骤
* `git add .`、`git commit -m "notes"`、`git remote add origin https://github.com/***/***.git`、 `git pull --rebase origin master`、`git push -u origin master`，顺序执行即可