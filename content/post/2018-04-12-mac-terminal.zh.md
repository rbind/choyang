---
title: Mac 终端配置
author: Yang
date: '2018-04-12'
slug: mac-terminal
categories:
  - Mac 
description: iterm2是一个Mac终端的替代品，功能非常强大，比如主题设置、分屏、复制、搜索等，使用起来非常方便。配置和安装iterm2和zsh。
---

iterm2是一个Mac终端的替代品，功能非常强大，比如主题设置、分屏、复制、搜索等，使用起来非常方便。配置和安装iterm2和zsh。

## 安装iterm2

从[iterm2 download page](https://www.iterm2.com/downloads.html)下载安装，或者利用[homebrew](https://brew.sh/)安装`brew cask install iterm2`.

##  配置iterm2

### 颜色主题

下载[主题](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/schemes). 按`Command + ,键`，打开 Preferences 配置界面，然后`Profiles -> Colors -> Color Presets -> Import`导入主题，然后再点击`Color Presets`选择主题即可。

> **注意**：如果主题背景色为浅色如`light background`，注意调整`Profiles -> Colors -> Minimum contrast`，不能太大

如果shell是使用的bash，还需要在`~/.bash_profile`中添加`export CLICOLOR=1`使主题颜色的正常美观。

### 快捷键

设置跳转至行首、行尾和单词跳转快捷键,&#x2318;&#x2190;, &#x2318;&#x2192;, &#x2325;&#x2190;, &#x2325;&#x2192;

`preferences -> profiles -> keys -> + ` 添加快捷键

- &#x2318;&#x2190;, action: `Send Esc Sequence`, send: `OH`
- &#x2318;&#x2192;, action: `Send Esc Sequence`, send: `OF`
- &#x2325;&#x2190;, action: `Send Esc Sequence`, send: `b`
- &#x2325;&#x2192;, action: `Send Esc Sequence`, send: `f`

## zsh 和 oh-my-zsh

Mac OS默认使用 bash shell，zsh比默认的bash功能更强大，如自动补全，颜色显示，历史命令，因为其配置复杂困难限制了它的使用。[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)用于配置zsh，可以很方便的管理插件，设置主题，所以使用zsh + oh-my-zsh可提高工作效率

### 安装zsh

安装zsh，shell修改为zsh

```sh
brew install zsh zsh-completions
chsh -s $(which zsh)
```

### 安装oh-my-zsh

```sh
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

### 配置oh-my-zsh

参考[Wiki页面](https://github.com/robbyrussell/oh-my-zsh/wiki/Customization)定制插件和主题，修改`~/zshrc`，如：

```
ZSH_THEME=pygmalion
plugins=(git colored-man colorize github jira vagrant virtualenv pip python brew osx zsh-syntax-highlighting)
```
配置环境变量，之前bash中`.bashrc`和`.bash_profile`中手动设置的环境变量都要在zsh中重新设置。

我们在`~/.oh-my-zsh/custom`中创建`env.sh`文件，专门用于自定义环境配置，在`~/.zshrc中`source ~/.oh-my-zsh.custom/env.sh`即可。如用sublime text配置`.zshrc`和`env.sh`，这样我们输入zshconfig即可打开sublime text进行配置。

```sh
# Use sublimetext for editing config files
alias zshconfig="subl ~/.zshrc"
alias envconfig="subl ~/.oh-my-zsh/custom/env.sh"
```


