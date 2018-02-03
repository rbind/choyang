---
title: 编译ggplot电子书
author: ''
date: '2018-02-03'
slug: compile-ggplot-book
categories:
  - R
tags:
  - ggplot
summary: "编译ggplot成PDF版本"
---

Hadley把他编写的**ggplot2: Elegant Graphics for Data Analysis**书的源文件晒到了
[Github](https://github.com/hadley/ggplot2-book)上。按照`README`编译过程中发现了
一些问题，所以将编译过程记录下来作为备忘。

##### 克隆库

```
git clone https://github.com/hadley/ggplot2-book.git
```

##### 安装依赖

- R开发工具，[R package development prerequisites](https://support.rstudio.com/hc/en-us/articles/200486498-Package-Development-Prerequisites)
- pandoc，[pandoc and pandoc-citeproc](http://pandoc.org/installing.html)
- 字体，[the Inconsolata font](http://www.ctan.org/tex-archive/fonts/inconsolata/)

安装包

```r
library(devtools)
if (packageVersion("devtools") < "1.9.1") {
  message("Please upgrade devtools")
}
devtools::install_deps('.')

# 需要注意的是编译ggplot需要bklamer的oldbookdown，不是bookdown
devtools::install_github("bklamer/oldbookdown")
```

##### 修改`/book/render-tex.R`

oldbookdown::tex_chapter() 中使用了参数`--chapters`，而目前**pandoc**已经把该参数改为`--top-level-division=chapter`，
修改`/book/render-tex.R`。

```R
library("methods") # avoids weird broom error
library("rmarkdown")

tex_chapter <- function (chapter = NULL, latex_engine = c("xelatex", "pdflatex",
  "lualatex"), code_width = 65)
{
  options(digits = 3)
  set.seed(1014)
  latex_engine <- match.arg(latex_engine)
  rmarkdown::output_format(rmarkdown::knitr_options("html", chapter),
    rmarkdown::pandoc_options(to = "latex",
      from = "markdown_style", ext = ".tex",
      args = c("--top-level-division=chapter",
      rmarkdown::pandoc_latex_engine_args(latex_engine))),
    clean_supporting = FALSE)
}

path <- commandArgs(trailingOnly = TRUE)
# command line args should contain just one chapter name
if (length(path) == 0) {
  message("No input supplied")
} else {
  base <- tex_chapter()
  base$knitr$opts_knit$width <- 67
  base$pandoc$from <- "markdown"

  rmarkdown::render(path, base, output_dir = "book/tex", envir = globalenv(), quiet = TRUE)
}
```

安装0.2.0版本**USAboundaries**

目前[cran](https://cran.r-project.org/web/packages/USAboundaries/index.html)上为0.3.0版本

```r
devtools::install_version(package = "USAboundaries", version = "0.2.0")
```

##### 编译

```r
cd ggplot2-book
make clean
make
```
PDF电子书生成`/book/tex/ggplot2-book.pdf`

##### Reference

[https://github.com/hadley/ggplot2-book/issues/134](https://github.com/hadley/ggplot2-book/issues/134)

