---
title: atom简介
author: Yang
date: '2017-04-16'
slug: atom-intro
categories: [atom]
tags:
  - atom
---


atom是github团队开发的一款编辑器，号称21世纪的编辑器。它吸收了很多目前最流行的编辑器sublime text的功能，如优美的界面、第三包包管理与安装，并且是基于web技术（chromium的框架）开发的一个开源编辑器，可扩展性强，配置简单。<!--more-->

### 安装

[atom的release页面](https://github.com/atom/atom/releases/tag/v1.16.0)下载系统相应的安装文件，如mac下为`atom-mac.zip`，解压拖动`atom.app`至应用程序文件夹，默认安装了`atom`终端命令和`apm`安装扩展包。


### 命令面板 - command platte

`cmd + shift + p`调出命令面板，可以搜索各种命令并执行（而不用手动查找）；此外，还可以查看命令是否有对应的快捷键。

### 偏好设置 - preferences

偏好设置面板，包括主题，字体，扩展包的安装等。三种打开方式：
  - `atom > Preferences`
  - `cmd+,`
  - 命令面板中，`settings-view:open`

### 主题 - theme

- UI theme: UI元素样式，如标签和树状图；
- syntax theme: 语法主题：代码高亮

### 空格和换行 - whitespace

- `soft tabs`，选中表示用空格代替`tab`，`tab length`则指定空格的个数；
- `soft wrap`, 行内字符过多时自动换行， `Soft Wrap At Preferred Line Length`，则表示每行最多80字符。


### 文件操作

#### 打开文件

- `file > open`
- `cmd + o`
- 命令行下：`atom [files]`

#### 编辑和保存

鼠标点击和修改是最简单的编辑操作，如果要高端地使用快捷键那么需要下载相应的扩展包，用于模仿其他文本编辑模式。

保存文件:`file > save`, `cmd + s`；另存为`file > save as`, `cmd + shift + s`; 保存所有文件`alt + cmd +s`

#### 打开文件夹

ATOM不限于编辑单个文件，而是旨在对项目中多个文件操作。

- `cmd + shift + o`添加文件夹到项目。
- `atom dir1 dir2`

打开文件夹后，左侧会出现文件目录树，方便对文件操作，包括打开，删除，重命名，新建文件。

`cmd + \`, 命令面板中`tree-view:toggle`打开或者关闭目录树。`ctrl + 0`会调整光标至目录树，`a`,`M`，`delete`用于添加、修改和删除文件或者文件夹。

> ATOM packages：目录树是不是直接植入ATOM，而是通过package实现，这种与ATOM捆绑的包称为核心包（core packages），区别于另外一种第三方的包（community packages）。

#### 打开项目中文件

- `cmd + t`或`cmd + p`在项目中模糊查找文件
- `cmd + b`在打开的文件中查找
- `cmd + shift + b`, 搜索上次git提交以来修改的文件或新文件

模糊匹配采用`core.ignoreNames,fuzzy-finder.ignoreNames`,`core.excludeVCSIgnorePaths`,配置设置来过滤掉不满足搜索条件的文件或者文件夹。所以如果项目中文件夹过多，我们可以自定义设置搜索路径或者`.gitignore`。
