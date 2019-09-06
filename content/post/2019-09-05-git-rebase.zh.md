---
title: git rebase 变基提交
author: ''
date: '2019-09-05'
slug: git-rebase
categories:
  - git
tags:
  - git
---

变基`rebase`主要与两个用途：分支之间commit的转移，可以把一个分支上的修改复制到另一个分支；交互式变基修改commit，如commit的合并、顺序调整、commit的提交日志修改。

### `git rebase -i`修改commit

```sh
# HEAD~3 指定可编辑的提交
git rebase -i HEAD~3
```
进入编辑器修改提交:

```sh
pick 383c7ee commit 3
pick 6b7b635 commit 2
pick 86b3e09 commit 1

# Rebase 7688f49..86b3e09 onto 7688f49 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
...
```

前三行就是选定的可修改的提交（由新到旧排列），每次提交前面都有个动词指定该提交的操作，默认为`pick`，下面`#`号开头的说明了其他的操作，如`reword`修改提交日志，`squash`将该提交合并到前一次提交。这样就可以编辑文本随意对提交进行排序、修改或删除等操作。

### 分支修改转移

一个分支通常是基于另一个分支（如master分支）进行开发，比如下图dev分支是从master分支的提交B处开始的，而后master分支又有了新提交C。

![](/post/2019-09-05-git-rebase/rebase-1.png)

可以修改使dev基于提交C保持dev基于最新版本的master分支开发，如在github fork了别人的仓库进行了修改，而后原始仓库又有了新提交，可使用变基使自己的提交移植到原始仓库的头。

```sh
# 默认是变基到当前分支
git checkout dev
git rebase master

# 或直接指定变基的分支
git rebase master dev
```

这样即可得到更新后的dev分支变成基于master的头开始，提交后面添加`'`表示与原始提交完全相同（原始提交被删除，然后新建相同的提交）。

![](/post/2019-09-05-git-rebase/rebase-2.png)

此外，还可以使用`--onto`选项把分支整个移植到其他完全无关的分支上。例如想把下图中的基于dev开发的feature分支上提交`F`和`G`移植到master分支上

![](/post/2019-09-05-git-rebase/rebase-3.png)

```sh
git rebase --onto master dev feature
```

提交后结果如下图所示

![](/post/2019-09-05-git-rebase/rebase-4.png)

在迁移多个提交时，实际上变基操作一次只迁移一个提交，因此，在变基的时候可以出现提交冲突，这时候会弹出编辑文本处理冲突，解决冲突后`git rebase --continue`可继续进行变基。`git rebase --abort`可随时终止变基。



