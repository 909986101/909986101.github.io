>hexo 官网：https://hexo.io/

>hexo 中文文档：https://hexo.io/zh-cn/docs/

# 环境搭建

## 安装 git

1. 下载：https://git-scm.com/download/win

1. 安装：step by step

## 安装 node.js

1. 下载：https://nodejs.org/en/

1. 安装：step by step  
注意：使用 Node.js 官方安装程序时，请确保勾选 Add to PATH 选项（默认已勾选）

1. 验证

       $ npm -v

   如果出现版本号，那说明安装成功了并且环境变量也配置好了

## 安装 hexo

1. 安装

       $ npm install -g hexo-cli

2. 验证

       $ hexo -v

# 构建

## 初始化

1. 安装

       $ hexo init blog.ilxy.tech
       $ cd blog.ilxy.tech
       $ npm install

## 安装 next 主题

1. 安装

       $ cd blog.ilxy.tech
       $ git clone https://github.com/theme-next/hexo-theme-next themes/next

## 安装插件

1. 安装流程图插件（可选）

       $ cd {blog_folder}
       $ npm install --save hexo-filter-mermaid-diagrams
       $ npm install --save hexo-filter-flowchart
       $ npm install --save hexo-filter-sequence

1. 安装本地搜索插件

       $ npm install hexo-generator-search --save

1. 安装 git 部署插件

       $ npm install hexo-deployer-git --save

# 配置

您可以在 _config.yml 中修改大部分的配置。

## 配置文件

1. 站点配置文件

       ...... ......
       ...... ......

       theme: next

       deploy:
         type: git
         repo: https://github.com/909986101/909986101.github.io.git
         branch: master

1. 主题配置文件

    路径：`themes/next/_config.yml`

# 部署

## 本地

1. 代码

       $ cd {blog_folder}
       $ hexo s

## 发布

1. 代码

       $ cd {blog_folder}
       $ hexo clean
       $ hexo g
       $ hexo d