# 环境准备

安装 git
```
# yum install git
```

安装 node.js 和 npm
```
# yum install nodejs npm
```

安装 hexo
```
# npm install -g hexo-cli
```

验证
```
# node -v
# npm -v
# hexo -v
```

# 本地 blog

初始化
```
# cd {blog_folder}
# hexo init
```

安装 next 主题
```
# cd {blog_folder}
# git clone https://github.com/theme-next/hexo-theme-next themes/next
```

安装流程图插件
```
# cd {blog_folder}
# npm install --save hexo-filter-mermaid-diagrams
# npm install --save hexo-filter-flowchart
# npm install --save hexo-filter-sequence
```

安装本地搜索插件
```
# npm install hexo-generator-search --save
```


```
# npm install hexo-deployer-git --save
```

# 配置文件

## 站点配置文件

```
# vim _config.yml
```
```yaml
theme: next

deploy:
  type: git
  repo: https://github.com/909986101/909986101.github.io.git
  branch: master
```

## 主题配置文件

```
# vim themes/next/_config.yml
```

# 使用

本地预览
```
# cd {blog_folder}
# hexo -s
```

发布
```
# cd {blog_folder}
# hexo clean
# hexo g
# hexo d
```