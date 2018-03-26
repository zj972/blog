---
layout: post
title: Cookie安全探索
author: Sarbo Yang
categories:
  - 编程人生
tags:
  - Cookie
date: 2018-03-14 17:46:32
---

在使用前端保存数据时，我通常会使用```LocalStorage```，相较于```Cookie```，前者更方便，容量更大，而且保存时间长。但是对于后端来说，我们同样需要在前端保存一些数据并与之交互，也就是在HTTP头中携带Cookie。

## Cookie的基本属性

* name（名称）
* value（值）
* domain（子域）
* path（站点路径）
* expires/Max-Age（过期时间）
* Size（大小）
* http（仅HTTP读取）
* secure（安全性）

具体的属性用法，网上都有介绍，就不一一赘述

## Cookie安全问题

* 不唯一：Cookie是由三元组[name, domain, path]来确定的，是会出现重名，即不是唯一的
* 易于获取：前面提到了Cookie是被携带在HTTP上面的，所以很容易从请求上截取到Cookie
* Cookie注入：容易截取的同时，Cookie也易于修改

## 思考

基于上面的问题，我有思考过当前我所做的项目存在的安全问题，虽然只是一个内部的管理页面，有内网限制。但公司员工如果发现安全漏洞，岂不是可以攻击系统了。

看了很多相关的博文，对我当前项目的Cookie进行了一些基础的防护：

* 将一些较为敏感的信息作为post请求字段进行传递
* 对系统的用户输入提交进行脚本过滤
* 设置secure为true
* 设置HTTPOnly属性
* 定期自动清理一些不必要的Cookie字段

END