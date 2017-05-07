---
title: Git 修改已提交commit 的 message
author: Yang
date: '2017-04-28'
slug: change-commit-message
tags:
  - git
---

偶然发现之前某次 `git commit `中message单词拼错了，作为完美强迫症患者，当然要找方法改之。
<!--more-->

`git rebase -i`允许对一些commit的整理和修改。如果对最近的三条 commit （或者其中的任意一条）进行修改：

`git rebase -i HEAD~3`

或者

`git rebase -i $head`

指定某次 commit头文件，则可以对该commit 之前的commit 进行编辑。随后编辑器里出现文件：

```
pick 2d1a960 an into to the website
pick 651c530 ignore and delete public dir
pick 67547b4 reset number of list posts to 8 in zh page

# Rebase 1cd4b97..67547b4 onto 1cd4b97 (3 command(s))
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
...
```

前三行列出了可以修改的 commit，每个提交前都有一个命令(默认为 `pick`）指定了作何修改，`pick`修改为`reword`来编辑 commit 的 message。

```
edit 2d1a960 an into to the website
pick 651c530 ignore and delete public dir
pick 67547b4 reset number of list posts to 8 in zh page
```
保存退出后，会自动滚回到列表中的最后一次提交，并出现以下提示语句：

```
Stopped at 2d1a960... an intro to the website
You can amend the commit now, with

	git commit --amend 

Once you are satisfied with your changes, run

	git rebase --continue
```

运行：

```
git commit --amend
```

第一行即是 commit 的 message

```
an intro to the website

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
...
```

修改保存，确认修改成功运行：

```
git rebase --continue
```
完成了修改某 commit 的 message，最后强制push到远程仓库完成本次任务。

```
git push --force
```

需要注意的是，对于多人协作的git 库，如果commit 已经 push，那么就将错就错，修改commit可能对开发者引发混乱。

