---
title: Hugo建立的网站托管至github pages
author: Yang
date: '2017-03-21'
slug: hugo
categories: []
tags:
  - blogdown
  - github
---

## github pages

[github pages](https://pages.github.com),[bitbucket](https://bitbucket.org/product),[gitlab](https://gitlab.com)是免费的可以用来搭建博客和托管项目网页的工具，这里我们选择最常用的github pages来托管网站。<!--more-->

github pages分为两类

- 个人或者机构账户主页，必须为`username.github.io`,只能在`master`分支中建立主页。
![](/post/2017-03-21-hugo-hosting-github/github_personal_page.png)
- 项目主页，可以在`master`分支，`master/docs`文件夹，`gh-pages`分支建立项目主页
![](/post/2017-03-21-hugo-hosting-github/github_project_page.png)


因此有以下几种方法将hugo网站托管至github pages

- 网站源文件与网站内容分别存在不同的仓库，内容保存在`uername.github.io`，源文件保存在`website-source`中，注意这里需要设置`publicDir="../username.github.io`。
- 网站源文件与网站内容同一个repo下的两个分支，master（网站内容）， source（网站源文件），选择master分支建立github pages
- 网站源文件与网站内容同一个repo下的两个分支，master（网站源文件）， gh-pages（网站内容），选择gh-pages分支建立github pages
- 一个分支，网站保存在master下的docs文件夹，选择`master/docs`建立githubpages，但这总情况只能选择项目主页，所以在构建个人站点的时候不适合。


明显第一种方法最简单，保存在不同分支中的做法涉及两个分支的操作，相信一般人对git分支操作比较头大（当然也包括俺），所以我本人选择了第一种方法来托管个人站点。<i>**详细建个人网站的人对于如何使用git和github应该有所了解**</i>


### 绑定域名

有些人想把github pages绑定到个人的域名。这就需要在网站根目录建立`CNAME`文件，写入自己的域名。然后按以下步骤配置域名：

- 设置主机记录`@`,记录类型为`CNAME`, 记录值为`yiluheihei.github.io.`注意后边有个点。 ,将`choyang.me`域名映射到`yiluheihei.github.io`

- 设置主机记录`www`，记录类型为`A`，记录值是IP `192.30.252.154`

- 设置主机记录`www`，记录类型为`A`，记录值是IP `192.30.252.153`，这两个是github pages的IP地址，访问这两个IP表示方位github pages

稍等一小会，域名`choyang.me`就可以访问，重定向到`yiluheihei.github.io`。

![](/post/2017-03-21-hugo-hosting-github/domain_setting.png)













