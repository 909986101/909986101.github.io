---
title: hexo 配置 添加 Live2D 看板娘
date: 2020-03-11 15:42:00
urlname: hexo-live2d
categories:
  - [hexo]
  - [live2d]
tags: [hexo, live2d]
---
hexo 配置 添加 Live2D 看板娘
<!--more-->
>参考：https://github.com/EYHN/hexo-helper-live2d/blob/HEAD/README.zh-CN.md

# hexo 添加 Live2D 看板娘

## 安装

安装模块

```
$ npm install --save hexo-helper-live2d
```

## 配置

请向Hexo的 _config.yml 文件或主题的 _config.yml 文件中添加配置

```yaml
live2d:
  enable: true
  pluginModelPath: assets/
  model:
    use: live2d-widget-model-epsilon2_1  #模板目录，在 node_modules 里
  display:
    position: right
    width: 150 
    height: 300
  mobile:
    show: false  #是否在手机进行显示
```

设置分为helper特有的和公共的, 你需要把他们合并放到 _config.yml 中

```yaml
# Live2D
## https://github.com/EYHN/hexo-helper-live2d
live2d:
  enable: true
  # enable: false
  scriptFrom: local # 默认
  pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/ # 模型文件相对与插件根目录路径
  # scriptFrom: jsdelivr # jsdelivr CDN
  # scriptFrom: unpkg # unpkg CDN
  # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
  tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false # 调试, 是否在控制台输出日志
  model:
    use: live2d-widget-model-wanko # npm-module package name
    # use: wanko # 博客根目录/live2d_models/ 下的目录名
    # use: ./wives/wanko # 相对于博客根目录的路径
    # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
```

## 模型

安装模型

```bash
$ npm install live2d-widget-model-epsilon2_1
## 一个夏装妹子, 比较适合宅男
```

# 进阶：能说话、能换装

>https://blog.csdn.net/qq_39610915/article/details/90679768