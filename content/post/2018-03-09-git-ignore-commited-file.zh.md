---
title: git忽略已提交的文件
author: ''
date: '2018-03-09'
slug: git-ignore-commited-files
categories: []
tags: [git]
---

`.gitignore`用于过滤掉不需要git控制的文件或文件夹。然而，`.gitignore`对于已经添加至版本库的文件不起作用，必须在版本库中删除相应文件/文件夹才能忽略它们。<!--more-->

```sh
# 删除文件夹的时候需要设置参数-r，--cached表示取消对该文件的追踪(track)
git rm -r --cached <File/Dir>
```

