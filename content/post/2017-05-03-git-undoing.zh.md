---
title: Git 撤销修改
author: Yang
date: '2017-05-03'
slug: git-undoing
categories: [git]
tags: [git]
---


git 修改文件的时候难免会出错，撤销修改是经常用到的操作，需要注意的是并不是所有的修改都是可逆的，所以操作需谨慎。<!--more-->

## 撤销已跟踪文件的修改

- 修改后未添加至缓存区`

    ```
    git checkout -- <file>
    ```   
    
- 已添加至缓存区 `git add`

    ```
    git reset HEAD <file>
    ```
    
- 已经提交 `git commit`

    直接撤销最近一次提交，
  
    ```
    git commit --amend
    ```

    按版本 ID 撤销提交，首先查看版本信息, 返回commit的SHA（每次提交的唯一ID) 和 message
  
    ```
    git log --pretty=oneline
    b6d09d73d3b941761db4698cb016e739a4d2b260 tweak zh page
    2c218b81807aa6c9388d99c633a1f14b5819cc48 tweak post title
    c5495a95b8817820ed10d99d0acc5e956b230f87 changing commit message
    ```

    HEAD表示最新版本即当前版本，所以它的id为`b6d09...d2b260`，`HEAD^`表示上一个版本，依次类推`^` 的个数 n表示第前n 个版本。接着使用`git reset`回退版本。

    ```
    # 回退到上一个版本
    git reset --hard HEAD^
  
    # 根据 id 回退到某个版本，写 id 前几位即可（推荐8位）
    git reset --hard <SHA>  
    ```

    **后悔药**：重新恢复到新的版本
    
    ```
    # 提取HEAD 的变化历史
    git reflog
    b6d09d7 refs/heads/master@{0}: commit: tweak zh page
    2c218b8 refs/heads/master@{1}: commit: tweak post title
    c5495a9 refs/heads/master@{2}: commit: changing commit message

    git reset --hard <SHA>
    ```

## 撤销未跟踪文件的修改（unstaged，新文件）

```
# -n 显示删除的文件或目录，-d 文件夹，-f 删除文件
git clean -ndf
git clean -df
```

> Git 会定期清理无用对象，所以长时间的操作历史可能会被删除，并不是所有的操作都是可逆的。


