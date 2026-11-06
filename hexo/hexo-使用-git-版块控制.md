---
title: hexo 使用 git 版块控制
date: 2020-03-11 15:34:01
urlname: hexo-use-git
categories:
  - [hexo]
  - [git]
tags: [hexo, git]
---
hexo 使用 git 版块控制
<!--more-->
# hexo 通过 git 进行版本控制

## 初次提交代码

```bash
$ cd <blog_folder>
```
```bash
$ git config --global user.email "909986101@qq.com"
$ git config --global user.name "909986101"
$ git config --global credential.helper store
```

初始化本地仓库

```bash
$ git init
```

将本地仓库和远程仓库进行关联

```bash
$ git remote add origin https://github.com/909986101/blog.ilxy.tech
```
```bash
$ git add .                                 ## 将本地代码加入暂存区
$ git commit -m "-"                         ## 将本地代码加入本地仓库
$ git push                                  ## 将本地分支push到远程仓库
$ git push --set-upstream origin master
```