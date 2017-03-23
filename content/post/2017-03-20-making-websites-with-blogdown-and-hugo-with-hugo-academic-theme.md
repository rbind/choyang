---
title: Making websites with blogdown and hugo with hugo-academic theme
author: 'Yang '
date: '2017-03-20'
slug: making-websites-with-blogdown-and-hugo-with-hugo-academic-theme
categories: []
tags:
  - R
  - blogdown
  - R Markdown
---

## Install blogdown and hugo

You can install the package via:

```r
devtools::install_github('rstudio/blogdown')
```

If you are not familiar with Hugo or the `PATH` variable, or do not want to read the Hugo installation instructions, you may use the helper function `blogdown::install_hugo()` to install Hugo. <!--more-->

## Create website with hugo-academic theme

Once you have installed Hugo, you may create a new site via `blogdown::new_site(theme='gcushen/hugo-academic')` under an empty directory. It will create a skeleton site, download a Hugo theme from Github, add some sample content, launch a web browser and you will see the new site.



## Customize your own website according to hugo-academic theme

由hugo构建的网站内容都是由**markdown**文本参考模板构成，其网站内容在`content`文件夹中。

- `config.toml`： `[[manu.main]]`链接至各个widget，可通过修改`weight`
值改变manu的顺序，`title`,`params`修改名称和个人信息等；

- 删除不必要文件，主页内容在`home`中，由多个widget构成，可以删除不必要的widget，`weight`表征了各个widget的显示顺序；

- 每个post的summary，加<code>&#60;&#33;&#45;&#45;more&#45;&#45;&#62;</code>或者在yaml加上`summary`参数。

- post、project等参数中（如`summary`，`abstract`）有`"`和`\`(LaTex中的`\times`)，需要用`\`转义，`\"`, `\\times`





