---
title: 更新Github中fork的repo
author: Yang
date: '2017-04-16'
slug: github-fork-repo
tags:
  - git
  - github
description: 更新在github上fork的别人的仓库。
---

更新在github上fork的别人的仓库。

1. clone 自己fork的 repo, 当然如果已有本地库关联至该 repo，直接跳至 repo 文件夹即可。

    ```
    # clone your forked repo
    git clone https://github.com/<your_username>/<forked_repo>
    cd into/cloned_forked_repo
    ```
    
1. 设置上游repo为原始用户的仓库，并抓取该仓库元数据

    ```
    # Add remote from original repository in your forked repository:
    git remote add upstream <https://github.com/<original_user>/<forked_repo>.git
    git fetch upstream
    ```

1. 更新数据：分为两种情况。
  
  - fork 的仓库中有自己的commit，变基合并然后推送
  
    ```
    # 合并指定的远程分支至当前活动分支
    git rebase <branch>
    git push 
    ```
  - 没有对 fork 的仓库做任何更改，直接拉取然后推送

    ```
    # 拉取指定的远程分支至当前活动分组
    git pull upstream <branch>
    git push
    ```
    
**2017/05/17更新**
