---
title: 将 github 与你的域名绑定
date: 2020-03-12 22:33:03
urlname: Configuration-a-custom-domian-4-github-pages-site
categories:
  - [hexo]
  - [github]
tags:
  - hexo
  - github
---
将 github 与你的域名绑定
<!--more-->
# 将 github 与你的域名绑定

## github

仓库设置中 Custom domain

```
ilxy.tech
```

## CNAME

```
ilxy.tech
```

注意：
- CNAME 文件名全大写
- 内容只能包含一个主机名，不建议用泛解析（*）

## 域名解析设置

增加一条记录

|项|值|
|:-|:-|
|记录类型|A|
|主机记录|@|
|记录值|yourname.github.io 的 ip|
