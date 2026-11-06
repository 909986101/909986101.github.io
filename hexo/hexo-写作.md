---
title: hexo 写作
date: 2020-03-11 15:50:02
urlname: hexo-Writing
categories: hexo
tags: hexo
---
hexo 写作
<!--more-->
# hexo 写作

## page

```yaml
---
title: {{ title }}
date: {{ date }}
comments: false
---
```

```bash
$ hexo new page about
$ hexo new page tags
$ hexo new page categories
$ hexo new page archives
```

## post

**post.md**

```yaml
---
title: {{ title }}
urlname:
date: {{ date }}
categories:
tags:
---
```