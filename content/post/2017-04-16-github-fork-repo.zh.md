---
title: 保持github中fork别人repo的更新
author: Yang
date: '2017-04-16'
slug: github-fork-repo
categories: []
tags:
  - git
  - github
summary: "更新github中fork别人repo"
---


1. Clone your fork:
```
git clone git@github.com:YOUR-USERNAME/YOUR-FORKED-REPO.git
```
1. Add remote from original repository in your forked repository:
```
cd into/cloned/fork-repo
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream
```

1. Updating your fork from original repo to keep up with their changes:
```
git pull upstream master
```
1. updated your local repo and need to push your changes:
```
git push
```

[https://gist.github.com/CristinaSolana/1885435](https://gist.github.com/CristinaSolana/1885435)
