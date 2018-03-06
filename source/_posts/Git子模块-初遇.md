---
layout: post
title: Git子模块-初遇
date: 2018-03-05 14:31:02
author: Sarbo Yang
categories:
    - 编程人生
tags:
    - Git
---

## 子模块

使用Git已经有好几年了，但是从来没有使用过Git的子模块，因为大多数项目都是独立的，项目之间并没有包含关系。所谓子模块，也就是将一个Git仓库作为另一个Git仓库的子目录，然后在大的仓库里进行模块化管理子仓库。

## 问题初探

在搭建Blog的过程中，有使用到Hexo的主题next，在提交代码到Git上时，发现next文件无法commit：

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

    modified:   themes/next (modified content)

no changes added to commit (use "git add" and/or "git commit -a")
```

看了一下网上的解释，原来是因为我是clone的代码，next文件下有.git的存在，只需要删除就可以。删除虽然可以解决问题，但这样就无法更新next了，如果下载后手动合并自己的修改又过于麻烦。而且由于我是深度修改了next，很多文件都进行了修改，所以无法像[issues](https://github.com/iissnan/hexo-theme-next/issues/328)那样，提取个人的配置，不对next进行修改。

## 子模块使用

这时候看到有人提到了fork+submodule的方法，大概意思就是将next项目fork到自己的GitHub上，然后clone下来并作为子模块进行管理，这样既可以修改next并上传保存，也可以update作者的代码。

### 操作步骤

先clone并建立子模块

```bash
$ git submodule add https://github.com/zj972/hexo-theme-next themes/next
```

进行完这一步操作就会clone仓库代码到对应路径，同时还会在根目录下生成一个.gitmodules文件，该配置文件保存着仓库链接和本地目录的映射关系：

```bash
$ cat .gitmodules
[submodule "themes/next"]
    path = themes/next
    url = https://github.com/zj972/hexo-theme-next
```

然后就可以进行子模块的修改和操作了，作为刚用上这个命令不太熟的，其实可以直接进入到子仓库目录下进行git操作。

一下是几条操作的示例：

查看详细的差异信息

```bash
$ git diff --cached --submodule
```

克隆包含有子模块的项目

```bash
$ git clone git@github.com:zj972/blog.git
```

这个时候子模块目录是空的，需要通过submodule进行更新

```bash
$ git submodule init
$ git submodule update
```

其他的子模块操作还在尝试中...

END
