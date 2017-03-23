---
title: "R code style"
date: "2014-11-04"
tags: [R]
---


R作为用于统计计算和图形可视化的高级语言，随着近来来大数据的发展，R语言逐渐成长为数据分析的利器，良好的代码风格使代码更容易阅读，
分享和扩展，下面基于Rstudio首席科学家<a href="http://had.co.nz/">hadley</a>和google的R团队的代码风格做了一些小的调整。<!--more-->

### 符号和命名

#### 文件名字
- *.R* 作为文件扩展名
- 文件的命名要与它的功能相关

  - GOOD: predict_ad_revenue.R
  
  - BAD: foo.R

<!-- more -->
  
#### 对象名称
标识符中不要含有*-* 和*_*, 变量名字使用小写, 词之间用*.* 分割(variable.name), varibaleName也可以, 个人偏向使用前一种; 函数名每个词第一个字母要大写 (FunctionName), 第一个词是动词, hadely目前是利用*_* ；因为R的方法调用都或者某些类的定义使用*.*,所以函数的定义不要使用*.*; 常量命名规则除了名字开头加个*k*其他与函数一致, (kConstantName) 


- variable.name is preferred, variableName is accepted 

  - GOOD: avg.clicks
  
  - OK: avgClicks
  
  - BAD: avg_Clicks
  
- FunctionName 

  - GOOD: CalculateAvgClicks 
  
  - BAD: calculate_avg_clicks , calculateAvgClicks
  
  - Make function names verbs.
  
  例外: When creating a classed object, the function name (constructor) and class should match (e.g.,lm).

- 常量：k加上常量名称，kConstantName

	当然不能使用R中自定义的已存在的函数和变量的名字

```r
# Bad
T <- FALSE
c <- 10
mean <- function(x) sum(x)
```

### 句法

#### 每行代码的字符数

不超过80个字符；如果发现自己的代码行超过80个字符，那么要考虑封装代码至一个简短函数，或者使用[magrittr](http://cran.r-project.org/web/packages/magrittr/vignettes/magrittr.html)包的管道操作符.

#### 缩进
两个空格, 不要用tab tab与空格一起使用

例外: 换行在一个括号内, 那么下一行开头和括号内第一个字符对齐

```r
long_function_name <- function(a = "a long argument", 
                               b = "another argument",
                               c = "another long argument") {
  # As usual code is indented by two spaces.
}
```

#### 空格
所有的二元操作符两边有一个空格(=, +, -, <-, etc.).

函数调用传递参数时候=号两边的空格可有可无, 个人觉得应该有空格

逗号之前不要有空格, 后面要加空格

`:`, `::` 和`:::` 两边不需要空格	

GOOD:

```r
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])
total <- sum(x[, 1])
total <- sum(x[1, ])
```

BAD:

```r
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])  # Needs spaces around '<'
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])  # Needs a space after the comma
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])  # Needs a space before <-
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])  # Needs spaces around <-
total <- sum(x[, 1])  # Needs a space after the comma
total <- sum(x[, 1])  # Needs a space after the comma, not before
```

  
括号之前加空格, 调用函数除外

GOOD: 

```r
if (debug)
```

BAD:

```r
if(debug)
```


额外的空格 比如为了使代码的等号或者(<-)对齐

```r
list(
  total = a + b + c, 
  mean  = (a + b + c) / n
)
```

括号和方括号的周围不要有空格
GOOD:

```r
if (debug) x[1, ]
```

BAD:

```r
if ( debug )  # No spaces around debug
x[1,]  # Needs a space after the comma 
```


#### 大括号
左大括号不要另起一行, 右大括号一定要另起一行, 代码块包含单独语句时括号可省略, 但是代码中大括号是否省略要保持一致

```r
if (is.null(ylim)) {
    ylim <- c(0, 0.06)
}
## xor (but not both)

if (is.null(ylim)) ylim <- c(0, 0.06)
```

代码块要另起一行

BAD:

```r
if (is.null(ylim)) ylim <- c(0, 0.06)
if (is.null(ylim)) {
    ylim <- c(0, 0.06)
}
```


#### 含else代码块要使用大括号

*esle* 语句与大括号要在同一行

```r
if (condition) {
  one or more lines
} else {
  one or more lines
}
```

BAD:

```r
if (condition) {
  one or more lines
}
else {
  one or more lines
}
```

BAD:

```r
if (condition)
  one line
else
  one line
```

如果条件语句后面跟着简短的语句则可以写在同行

```r
if (y < 0 && debug) message("Y is negative")
```


#### 分号

行尾不要使用分号, 不要使用分号将多个语句放在同一行

### 组织

#### 总体布局和顺序

1. 版权声明
2. 作者
3. 文件说明注释, 包括文件是用来做什么以及输入输出的说明
4. `source()` 和`library()`语句
5. 函数定义
6. 执行语句, 也就是example (e.g., print, plot)

附加单元测试文件*originalfilename_test.R*

#### 注释

注释行以一个#开头, 加一个空格, 注释要说明为什么写这行代码（不是代码做了什么）

有时候会使用注释把代码分割成若干易读和理解的代码块，使用

```r
# =================================================================
# why this code
# =================================================================
```

```r
# Create histogram of frequency of campaigns by pct budget spent.
hist(df$pct.spent,
     breaks = "scott",  # method for choosing number of buckets
     main   = "Histogram: fraction budget spent by campaignid",
     xlab   = "Fraction of budget spent",
     ylab   = "Frequency (count of campaignids)")
```


### 函数

函数的名称一般为动词；函数中的代码块应该可以在一个屏幕上阅读（二三十行）

####调用

没有缺省值的参数应该放在前面, 后面跟着有缺省值的参数

函数定义及调用允许一行多个参数, 换行符要在参数之间

GOOD

```r
PredictCTR <- function(query, property, num.days,
  show.plot = TRUE)
```

BAD

```r
PredictCTR <- function(query, property, num.days, show.plot =
  TRUE)
```

单元测试作为函数的example

#### 文档

函数应该包含注释块紧接着函数定义的行(函数体), 包含了函数的说明, 参数的使用, 返回值, 建议使用(roxygen2)[http://cran.r-project.org/web/packages/roxygen2/index.html]的模式, 便于开发package,**rstudio**已经很好的整合了**roxygen2**。

#### 自定义函数

```r
CalculateSampleCovariance <- function(x, y, verbose = TRUE) {
  #' @description des description Computes the sample covariance between two vectors.
  #' @author  
  #' @param x: One of twovectors whose sample covariance is to be calculated.  
  #' @param y: The other vector.
  #' @param verbose ....
  #' @details x and y must have the same length, greater than one, with no missing
  #'  values.  verbose: If TRUE, prints sample covariance; if not, not. Default
  #'  is TRUE.  Returns: The sample covariance between x and y.
  #' @return ..
  #' @examples
  #' @importFrom
  
  n <- length(x)
  # Error handling
  if (n <= 1 || n != length(y)) {
    stop("Arguments x and y have different lengths: ", length(x), " and ", 
      length(y), ".")
  }
  if (TRUE %in% is.na(x) || TRUE %in% is.na(y)) {
    stop(" Arguments x and y must not have missing values.")
  }
  covariance <- var(x, y)
  if (verbose) 
    cat("Covariance = ", round(covariance, 4), ".\n", sep = "")
  return(covariance)
}
```





**此外**：绝对不要使用,attch的使用会使对象中的变量加载到相应的父环境中，可能会出现同名变量对象



### Ref

- [Hadley Wickham](http://stat405.had.co.nz/r-style.html)
- [CRAN](http://cran.r-project.org/doc/manuals/R-ints.html#R-coding-standards)
- [formatR](http://cran.r-project.org/web/packages/formatR/index.html)
- [Colin Gillespie](http://csgillespie.wordpress.com/2010/11/23/r-style-guide/)
- [Bioconductor](http://wiki.fhcrc.org/bioc/Coding_Standards)

