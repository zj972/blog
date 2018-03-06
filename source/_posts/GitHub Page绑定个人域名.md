---
layout: post
title: GitHub Page绑定个人域名
date: 2018-03-02 10:23:20
author: "Sarbo Yang"
categories:
    - 编程人生
tags:
	- GitHub
---
## 前情提要

自己的服务器到期了，然后打算在GitHub上面搭个个人博客玩玩，最后选择了Hexo。搭建起来后，用自己的域名绑定了GitHub Page。

但是遇到一个问题：每次`hexo d -g`之后，访问`www.yangshaobo.cn`就变成了404。DNS解析是正常的，打开项目的setting，却发现`Custom domain`的值为空。

<div align=center>
![404](http://img.yangshaobo.cn/404.png)
</div>

## 发现问题

原来当你添加个人域名时，GitHub会向你的项目仓库添加一个文件`CNAME`，里面包含了一个域名：

```text
www.yangshaobo.cn
```

而每次我使用通过Hexo部署时都会自动提交`public`文件夹到仓库里，配置信息如下：

```yaml
deploy:
  type: git
  repository: git@github.com:zj972/zj972.github.com.git
  branch: master
```

这样就把`CNAME`文件自动覆盖了。

## 解决方案

解决办法就是把`CNAME`文件添加到`source`文件夹里，这样每次部署就不会覆盖掉了。