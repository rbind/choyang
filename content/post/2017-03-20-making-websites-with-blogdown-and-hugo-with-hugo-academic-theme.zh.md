---
title: 利用hugo和blogdown创建网站
author: 'Yang '
date: '2017-03-20'
slug: 
categories: [hugo]
tags:
  - hugo
  - blogdown
---


hugo是一个可以快速建立静态网站的生成器，比如个人主页、博客、公司主页、项目介绍等。相对于其他静态网站生成器，hugo具有安装方便，网页编译生成速度快、实时刷新页面等特点。blogdown则整合了Rmarkdown和hugo的功能来帮助人们在R环境中建立网站（当然也可以是markdown）。<!--more-->

## 安装工具

下载安装R和Rstudio（相信常用R的自己电脑上必然已经装好了），然后安装R包blogdown。

```r
devtools::install_github('rstudio/blogdown')
```

随后`blogdown::install_hugo()`可以用来安装hugo，当然也可以根据自己的操作系统从hugo官网安装，详细步骤参见https://gohugo.io/overview/installing/。


## 选择academic主题建站

hugo提供了很多主题来建立网站， 参照http://themes.gohugo.io 选择自己喜欢的主题，我们选择`hugo-academic`主题。首先创建一个空文件夹构建网站，所以可以用Rstudio来创建一个Project。然后利用下面代码会在根目录下创建网站的源代码，主要包括：

 ```r
 blogdown::new_site(theme='gcushen/hugo-academic')` 
```
- `contig.toml`：网站的配置文件，如baseurl，title等，不同主题可设置的参数也不同，具体可查看主题的说明文档；
- `./archetypes`：包括内容类型，在创建新内容时自动生成内容的配置
- `./themes`: 选定的主题；
- `./layout`: 网站的模板`template`，设定了网站的展现形式；
- `./content`:根据模板生成的网站的内容，采用markdown格式，关于[template](https://gohugo.io/templates/overview/)以后会详细介绍。
- `./static`文件夹：css、js、img、media等，决定网站的外观


然后运行`blogdown::server_site()`就会生成站点，可以部署至服务器访问，默认根目录建立`public`文件夹来存储站点，可以设置`confog.toml`文件中的`publishDir`参数来修改。


## 个性化设置

随后可根据实际情况修改站点，由hugo构建的网站内容都是由**markdown**文本参考模板构成，其网站内容在`content`文件夹中。

- `config.toml`
  - `baseurl`:加你站点的网址，如`yiluheihei.github.io`;
  - `title`: 网站名称；
  - `theme`: 主题；
  - `params`: 个人信息和`contact`上显示的信息；
  - `[[manu.main]]`链接至各个widget，可通过修改`weight`
值改变manu的顺序；
  - `publishDir`：hugo生成网站的目录，默认为`./public`文件夹；我个人是把hugo源文件和生成的网站分别保存在两个repo：`personal-website-source`和`yiluheihei.github.io`，因此`publishDir = "../yiluheihei.github.io"`；

- 删除不必要文件，主页内容在`home`中，由多个widget构成，可以删除不必要的widget，`weight`表征了各个widget的显示顺序；

- 每个post的summary，加<code>&#60;&#33;&#45;&#45;more&#45;&#45;&#62;</code>或者在yaml加上`summary`参数。

- post、project等参数中（如`summary`，`abstract`）有`"`和`\`(LaTex中的`\times`)，需要用`\`转义，`\"`, `\\times`

<i>**当然不同的theme的参数也不同，上述都是针对`hugo-academic`主题板设置，要根据具体的主题来设置网站的参数。**</i>





