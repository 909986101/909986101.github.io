---
title: hexo 配置 压缩
date: 2020-03-11 15:46:59
urlname: hexo-Configuration-tune
categories: hexo
tags: hexo
---
hexo 配置 压缩
<!--more-->
# hexo 优化压缩

## hexo-neat

>参考：https://github.com/rozbo/hexo-neat

**安装模块**

```bash
$ npm install hexo-neat --save
```

**_config.yml**

```yaml
# hexo-neat
# 博文压缩
neat_enable: true
# 压缩html
neat_html:
  enable: true
  exclude:
# 压缩css  
neat_css:
  enable: true
  exclude:
    - '**/*.min.css'
# 压缩js
neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '**/*.min.js'
    - '**/jquery.fancybox.pack.js'
    - '**/index.js'
```