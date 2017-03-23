---
title: hugo网站部署
author: Yang
date: '2017-03-21'
slug: hugo
categories: []
tags:
  - blogdown
summary: 由blogdown和hugo建立的网站部署至github
---

## 上传至github

在website的跟目录git版本控制

```
git init
```

用wercker来控制网站的生成`public`文件夹

```
echo "/public" >> .gitignore
```

提交

```
git commit -a -m "Initial commit"
```

在github上建立一个仓库并与website文件夹关联

```
git remote add origin https://github.com/yiluheihei/personal-hugo-website.git

git push -u origin master
```

## wercker

用github注册wercker，并关联

点击页面顶端`create - application`选择关联的仓库

创建一个`cercker.yml`并push

### adding a deploy pipeline












