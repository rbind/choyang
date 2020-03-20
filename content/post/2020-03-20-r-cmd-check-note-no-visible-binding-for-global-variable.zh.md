---
title: '如何解决 R CMD check 出现  NOTE: "no visible binding for global variable"'
author: ''
date: '2020-03-20'
slug: r-cmd-check-note-no-visible-binding-for-global-variable
categories:
  - R
tags:
  - R
---

NSE (非标准话求值) 允许直接对数据的变量进行操作，如`subset()`函数。虽然初始目的是为了交互运行的时候减少代码输入方便计算，随着 tidyverse 兴起，大大增加了数据分析
效率，NSE 用途也越来越广，许多新开发的包都依赖一些采用了 NSE 的函数。在 `R CMD check`的时候出现 就出现由 NSE 引起的 NOTE `no visible binding for global 
variable, Undefined global functions or variables <variable name>`。这是由于
实际函数运行环境中并不包含这些变量，所以在`R CMD check` 的时候会抛出NOTE。虽然 
CRAN 中允许有NOTE，为了维护方便最好是把 NOTE 也都解决。有两种解决办法。

#### 1. 用`globalVariables(c("<var>"))`, 如可以在`R/`下新建一个脚本，调用
`globalVariables()`声明所有变量

  常用的是通过`.onLoad`函数：

  ```R
  .onLoad <- function (libname, pkgname)
  {
    # set global variables in order to avoid CHECK notes
    utils::globalVariables ("<var>")
    invisible ()
  }
  ```

#### 2. 使用`rlang::.data`,记得依赖中加入`rlang`和导出`.data`，以`dplyr::filter`为例

  ```R
  dplyr::filter(df, var > 1)
  # 修改为
  dplyr::filter(df, .data$var > 1)
  ```

我之前是采用的第一种方法，但是总是忘记哪些变量变量需要添加，现在采用第二种方法
在写代码的时候直接用`.data`，缺点就是跟平时交互式计算的时候写法不一致，有时候也
会忘记。

#### Reference

- [How can I handle R CMD check “no visible binding for global variable” notes when my ggplot2 syntax 
is sensible?](https://stackoverflow.com/questions/9439256/how-can-i-handle-r-cmd-check-no-visible-binding-for-global-variable-notes-when)
- [programming with dplyr](https://dplyr.tidyverse.org/articles/programming.html)
