---
title: Mac 升级 R 3.4.0 出现错误
author: Yang
date: '2017-04-25'
slug: mac-r-3.4.0-error
tags:
  - R
---

前几天CRAN 发布了R 3.4.0版本，今天抽空安装了下，然而重启 Rstudio 运行的时候，加载某些包（如 `dplyr`，`devtools`）出现错误`caught segfault  address 0x18, cause 'memory not mapped'`。

重新安装包也不起作用，想到自己升级到R 3.4.0的时候采用的覆盖安装，所以考虑可能是因为版本问题引发的这个错误。随后尝试按照[R-admin](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Uninstalling-under-macOS)的步骤完全卸载旧版本 R

```
sudo rm -rf /Library/Frameworks/R.framework /Applications/R.app \
   /usr/local/bin/R /usr/local/bin/Rscript
```

然后重新安装 R 3.4.0，问题解决，都是懒惰图省事覆盖安装的锅！然而，引发这个错误的根本原因是什么呢？

