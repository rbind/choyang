---
title: git忽略已提交的文件
author: ''
date: '2018-03-09'
slug: git-ignore-commited-files
categories: []
tags: [git]
---

`.gitignore`用于过滤掉不需要git控制的文件或文件夹。然而，`.gitignore`对于已经添加至版本库的文件不起作用，必须在版本库中删除相应文件/文件夹才能忽略它们。<!--more-->

用`git rm --cached`, --cached表示取消对该文件的追踪(track), 文件状态置为Untracted files， 工作区中仍保留, 从版本库中删除该文件，

```sh
# 文件夹加参数-r
git rm -r --cached <File/Dir>
```
然后将该文件添加至`.gitignore`即可。

