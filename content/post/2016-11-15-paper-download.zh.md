---
title: 文献下载
date: "2016-11-15"
tags: [scholar]
summary: "简要介绍自己经常用的`Google`学术搜索镜像和文献全文下载方法"
---

快速的找到自己研究方向或者感兴趣的文献，常常事半功倍，能很大的提高我们的工作效率，对于毕业论文和科研论文的写作也非常有用。由于XXX原因`Google`被和谐，`pubmed`能搜索生物医学领域文献，并且不太稳定经常XXX。至于后起之“秀”度娘学术和微软必应学术搜索，不论在搜索数量、质量和功能与`Google`学术都没有可比性，也许它们与`Google`学术之间的差距要比中美学术之间的差异还要大。下面道一道我经常用的`Google`学术搜索镜像和文献全文下载方法**(许多非开源杂志主页不提供全文下载)**。<!--more-->


## 目前俺常用的Goolge学术镜像

目前有许多`Google`学术镜像可以使用,俺常用的镜像有有下面几个，当然有其他更好的镜像就更好了。俺一般先使用比较稳定方便的`Glgoo`学术搜索，如果`Glgoo`被和谐，再尝试其他两个`Google`学术搜索导航。

1. `Glgoo`学术搜索:速度非常快，用很久了比较稳定
    - http://xueshu.glgoo.org
    - http://scholar.glgoo.org
2. [虫部落404BUS](www.404bus.com)： http://www.404bus.com
3. [思谋学术](http://dir.scmor.com/google/)：http://dir.scmor.com/google/
`Google`学术搜索导航包含很多`Google`学术镜像，可以选择使用。

## Google学术搜索

`Google`作为搜索引擎中的老大有很多搜索技巧，掌握一些常见的搜索技巧可以很大的提高工作效率，下边举几个常用例子（更多的说明可以看`Google`帮助）

- 在搜索词上加上双引号就表示精确搜索，显示与搜索关键词完全匹配的结果
- 按作者搜索，限定作者进行搜索:`[作者："knuth"]`,搜索作者姓名中含knuth的结果
- 减号表示搜索结果不包含减号后边的词，减号前有空格，后面没有：`[作者："knuth"] -DE`表示搜索结果中不能包含词`"DE"`

一些条件限制搜索位置，如`intitle`、`inurl`等限定搜索标题和url地址；`filetype`限制搜索结果的类型；`AND` 或者 `OR`组合多种搜索条件；等等等
    
很多杂志的文章在主页上不提供全文下载的，俄罗斯某网站`sci-hub`提供文献全文下载，个人使用中感觉除了一些新上线的文献外，`sci-hub`都可以搞定。常用镜像有：

- 国内`sci-hub`：
    - 主网址：http://www.sci-hub.cn
    - 备用网址：http://www.sci-hub.xyz

- 国外`sci-hub`镜像
    - http://www.sci-hub.cc/
    - http://www.sci-hub.bz/
    

1. 利用`PMID`号或者`DOI`下载全文

如果在`PubMed`查询到的文献，每篇文献都有一个`PubMed`号，我们可以复制这个号码在`sci-hub`进行查询。注意是`PubMed`号，而不是`PMCID`号。这样就可以打开`PDF`了。此时可能是自动下载`PDF`，或者打开新的PDF预览网页进行手动下载（图1）。

![](/post/2016-11-15-paper-download/PMID.png)


如果是在其他数据库或者杂志主页查询到的文献，可以利用文章`DOI`号在`sci-hub`下载到全文。方法同`PMID`,比如`DOI`号为`10.1016/j.jcv.2015.05.022`，输入`DOI`号搜索即可打开文章`pdf`页面

2. 利用关键词下载全文：直接输入关键词即可

3. 手动下载`PDF`全文

`sci-hub`网址样式为`http://www.xxx.com.sci-hub.cc/x/xx/xx/xx`。如`Nature`文章
`Astronomy: A Mars-sizedexoplanet`不提供全文下载，文章网址是：
http://www.nature.com/nature/journal/v522/n7556/full/522290a.html，
根据`sci-hub`的规则，改成如下样式：http://www.nature.com.sci-hub.cc/nature/journal/v522/n7556/full/522290a.html，
即可下载。


**注意**：`sci-hub`可能在部分地区部分网络可能出现访问受限的问题，`sci-hub`的开发人员会及时处理该问题，所以稍等待修复即可。

## Library Genesis

[Library Genesis](http://gen.lib.rus.ec/):(http://gen.lib.rus.ec/)提供下载
电子书、科技论文专利等，它集成了`sci-hub`的功能。搜索条件与`sci-hub`类似，科技论文搜索只要选中`scitific articles`选项即可，可以输入`PMID`，`DOI`或者关键词搜索（图2）。

![](/post/2016-11-15-paper-download/genesis.png)

点击`libgen`进入下载界面，下载即可（图3）。

![](/post/2016-11-15-paper-download/genesis2.png)

## 推荐步骤

1. `Glgoo`学术镜像查找文献：`Glgoo`比`sci-hub`稳定，所以推荐先使用`Glgoo`学术镜像查找
2. 杂志主页不提供全文下载的文献，使用`sci-hub`镜像下载（先国内再国外）
3. `sci-hub`不稳定登录不上去的时候，考虑使用`library genesis`下载。

## 穿墙术

利用穿墙术可以跳上墙头直接看到`google`，而不用使用`google`镜像，两种使用较多的免费翻墙工具（有钱人可以直接买`vpn`）：

1. xx-net： 详细教程见[https://github.com/XX-net/XX-Net/wiki/中文文档](https://github.com/XX-net/XX-Net/wiki/中文文档)

2. 蓝灯： 详情见[https://github.com/getlantern/forum](https://github.com/getlantern/forum)


