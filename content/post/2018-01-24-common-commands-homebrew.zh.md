---
title: Homebrew常用命令
author: Yang
date: '2018-01-24'
slug: common-commands-homebrew
categories:
  - Mac OS
tags:
  - Homebrew
description: "Homebrew常用命令，记下来以备查看"
---

Homebrew常用命令，记下来以备查看.
 
- `brew search text|/text/`, 搜索软件，支持正则表达式
- `brew install formula`, 安装软件
- `brew list`, 列出已安装的软件
- `brew info *`, 列出安装的某软件的详细信息
- `brew update`, 升级最新版本的homebrew，并从github获取新版本的软件信息，随后的`brew outdated|upgrade|cleanup`才有意义
- `brew outdated`, 查看哪些软件有新版本，可以进行升级
- `brew upgrade`, 升级所有有新版本的软件，或者指定某个软件进行升级`brew upgrade formula`， `--cleanup`选项表示是否删除旧版本软件
- `brew cleanup`, 删除旧版本的软件及其安装包，也可以指定某个软件，跟`brew upgrade`中`--cleanup`参数类似

综上，升级党一般的流程是
```sh
# 更新 Homebrew ，及软件列表
brew update     
# 列出过期软件    
brew outdated
# 升级所有过期软件或者指定某个软件   
brew  upgrade 
brew  upgrade <formula>
# 当然可以最后清理旧版本
brew cleanup 
```


