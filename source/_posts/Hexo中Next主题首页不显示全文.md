---
layout: post
title: Hexo中Next主题首页不显示全文
author: Sarbo Yang
categories:
  - 编程人生
tags:
  - Hexo
  - hexo-theme
  - theme-next
date: 2018-03-14 18:01:48
---

使用Next主题时，会发现它在首页默认是会显示全文的，这就很不方便浏览文章列表。

## 解决办法

找到主题配置文件```themes/next/_config.yml```，搜索```auto_excerpt```：

```yml
# Automatically Excerpt. Not recommend.
# Please use <!-- more --> in the post to control excerpt accurately.
auto_excerpt:
  enable: fales
  length: 150
```

将```enable```的值修改为```true```，而```length```是指显示的字数，然后重新部署就可以了~

Tips：使用预览会忽略文章的格式，直接显示为正文文本。

<div align=center>
![auto_excerpt](http://img.yangshaobo.cn/auto_excerpt.png)
</div>
