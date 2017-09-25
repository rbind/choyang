--- 
title: "数据结构"
date: "2017-09-24"
---

R 中常用的基础数据结构根据数据的维度（1维，2维，n维）和元素的性质（元素的类型是否相同 - 异质或同质）可分为以下几种：

|   |    同质                   |     异质
|---|---------------------------|---------------------
|1维|原子向量 - atomic vector   |列表   - list       |
|2维|矩阵     - matrix          |数据框 - data frame |
|n维|数组     - array           |                    |

其他复杂的类型的数据都是基于以上5种类型构建的.另外，R中不存在标量（0维数据，单个数字或字符），用长度为1的向量表征。函数`str()`（structure）用于显示对象的内部结构.

## 向量

向量是 R 中最基本的数据结构，分为原子向量(atomic vector)和列表(list)两类，其中原子向量所有元素的类型必须一样，而列表则允许元素具有不同的数据类型。向量的三个基本特征为:

- 类型: `typeof()`,其元素的类型.
- 长度: `length()`,元素个数.
- 属性： `attributes()`,额外的元数据.

**`is.vector()`仅当对象不含有属性（names 属性除外）的时候返回`TRUE`. `is.atomic(x) || is.list(x)`用于判断对象是否为向量.**

**`mode()`和`storage.mode()`返回对象的模式(mode)或存储模式，是从 S 语言继承下来的函数，可以忽略，其中`storage.mode()`与`typeof()`作用一致.**

### 原子向量

常见的原子向量有四种:logical,integer,double (numeric),character,此外，使用较少的 有complex和raw两种.原子向量用`c()`来创建.


```r
c(1.5, 2, 3)  # numeric
c(1L, 2L)     # L 表征为integer
c(TRUE, FALSE) # logical
c("a", "b") # char
```

缺失值`NA`是一个长度为1的逻辑向量,不同类型的向量中`NA`的类型也不同根据向量中元素的类型可分为 `NA_real_`, `NA_integer_`, `NA_character_`.

#### 类型判断

`typeof()`用来显示对象的类型，`is.*()`可用来判定对象是否是某一特定类型:`is.character()`, `is.double()`, `is.integer()`, `is.logical()`, `is.atomic()`.

需要注意的是is.numeric当数据位integer或double时都返回TRUE

#### 强制转换

如前所述原子向量中元素的类型必须相同，当利用不同类型的数据创建向量时，向量中的元素都会被强制转化为最灵活的数据类型，由低到高的顺序为logical, integer, double, character.



```r
c("a", 1) # 数值转化为字符
```

```
## [1] "a" "1"
```

```r
c(1L, 2.5) # 整形转化为实数
```

```
## [1] 1.0 2.5
```

```r
c(TRUE, FALSE, 1) # TRUE、FALSE分别为1和0
```

```
## [1] 1 0 1
```

### 列表

`list()`用于创建可包含不同类型元素的列表.


```r
x <- list(1:3, "a", c(TRUE, FALSE, TRUE), c(2.3, 5.9))
str(x)
```

```
## List of 4
##  $ : int [1:3] 1 2 3
##  $ : chr "a"
##  $ : logi [1:3] TRUE FALSE TRUE
##  $ : num [1:2] 2.3 5.9
```

列表也称为recursive（递归）向量，因为list的元素也可以是list. `c()`可以把多个列表合成一个，与 `list()`不同的是它会在合并之前把原子向量强制转化为列表.



```r
x <- list(list(1, 2), c(3, 4))
y <- c(list(1, 2), c(3, 4))
str(x)
```

```
## List of 2
##  $ :List of 2
##   ..$ : num 1
##   ..$ : num 2
##  $ : num [1:2] 3 4
```

```r
str(y)
```

```
## List of 4
##  $ : num 1
##  $ : num 2
##  $ : num 3
##  $ : num 4
```


相关函数：

- `is.list()`,判断是否为列表.
- `as.list()`, 强制转换为列表.
- `unlist()`，转化为原子向量.

列表用于存储复杂的数据，比如数据框是基于列表创建的一类数据.

## 属性

任意R对象都可包含额外属性来存储元数据，属性用列表表示（必须含有 names 属性，且 names不能重复, `attr()`提取特定名字的属性，`attributes()`列出对象的所有属性.


```r
y <- 1:10
attr(y, "my_attribute") <- "This is a vector"
attr(y, "my_attribute")
```

```
## [1] "This is a vector"
```

```r
attributes(y) #属性列表
```

```
## $my_attribute
## [1] "This is a vector"
```

`structure()`返回一个新的修改属性后的对象，S3类就是根据这个函数来定义.

修改向量时，默认丢弃除names，dimension和class(s3类)三种属性之外的所有属性. R 中额外定义了函数来访问和修改这三个属性, `names()`, `dim()`, 和`class()`.

### 名字属性

三种方法可以定义 names 属性

- 创建向量时，`x <- c(a = 1, b = 2, c = 3)`
- 修改已有向量，`x <- 1:3; names(x) <- c("a", "b", "c")`
- 根据已有向量创建修改的副本，`x <- setNames(1:3, c("a", "b", "c"))`

三种定义向量 names 的方法对缺少 names 的元素影响各不相同.

- .
- 修改已有向量的时候某些元素没有设置 names，这些元素的 names 为`NA`，如果所有元素都没有 names 那么`names(x)`返回`NULL`.


```r
# names 为空字符
y <- c(a = 1, 2, 3)
names(y)
```

```
## [1] "a" ""  ""
```

```r
# 修改已有向量的时候某些元素没有设置 names，这些元素的 names 为`NA`
v <- c(1, 2, 3)
names(v) <- c('a')
names(v)
```

```
## [1] "a" NA  NA
```

```r
# 所有元素都没有 names 那么`names(x)`返回`NULL`
z <- c(1, 2, 3)
names(z)
```

```
## NULL
```


### 因子

因子是通过设置 attributes 来定义的S3类，用于存储分类数据，实际上是一个必须包含预定义值的整形原子向量.基于整形向量，通过设置 class 和 levels（预定义值） 两个属性创建因子.


```r
x <- factor(c("a", "b", "b", "a"))
x
```

```
## [1] a b b a
## Levels: a b
```

```r
class(x)
```

```
## [1] "factor"
```

```r
levels(x)
```

```
## [1] "a" "b"
```

```r
typeof(x)
```

```
## [1] "integer"
```

需要注意的是，当我们从文件读取数据定义一个数值型df时，如果数据中含有特殊字符（非数字) 如“.”，“-”等，那么默认情况下这一列会转化为factor而不是数值型向量，可以通过先把它转化为character然后再转化为数值型向量来正确展示该元素. 还可以通过设置参数`na.strings`来解决该问题.


```r
z <- read.csv(text = "value\n12\n1\n.\n9")
typeof(z$value)
```

```
## [1] "integer"
```

```r
as.double(z$value) # 3, 2, 1, 4是因子的 level 的索引，而不是读入的数值
```

```
## [1] 3 2 1 4
```

```r
class(z$value)
```

```
## [1] "factor"
```

```r
as.double(as.character(z$value)) #先转化为字符向量，在转化为数值型
```

```
## Warning: NAs introduced by coercion
```

```
## [1] 12  1 NA  9
```

```r
# 设置 `na.strings`
z <- read.csv(text = "value\n12\n1\n.\n9", na.strings = ".")
typeof(z$value)
```

```
## [1] "integer"
```

```r
class(z$value)
```

```
## [1] "integer"
```

```r
z$value
```

```
## [1] 12  1 NA  9
```

**R 中几乎所有的数据读入函数默认情况下，会把字符型数据转化为因子.为了避免不需要的麻烦，可以设置参数`stringsAsFactors = FALSE`,然后需要factor时候再转化.

虽然因子看起来像字符向量，实际上他们是以整型存储的，所以在对因子做字符处理的时候，强烈建议先把它转化为character.**

## 矩阵和数组

基于原子向量，设置dim属性，可以构建多维数组、矩阵(2维数组)，矩阵实际上是数组的特例（二维）. `matrix()`和`array()`用于构建矩阵和数组.


```r
a <- matrix(1:6,3)
b <- array(1:12, c(2, 3, 2))

# 原子向量设置 dim 属性
c <- 1:6
dim(c) <- c(3, 2)
```

常用函数

- `nrow()`,`ncol()`，`dim()`:行列数
- `colnames()`,`row.names()`:元素名称
- `dimnames()`:列表，对数组元素命名
- `cbind()`,`rbind()`,`abind()`:合并
- `t()`,`aperm()`：转置
- `is.*()`,`as.*()`,类型判断和转化

此外，基于列表设置dim属性可以构建列表矩阵或者数组


```r
l <- list(1:3, "a", TRUE, 1.0)
dim(l) <- c(2, 2)
```

## 数据框

数据框是基于列表创建的 S3类，因此 `typeof(df)`为 `list`. 数据框中是由一系列相同长度的向量构成,构成了一个2维数据，因此可以称之为向量列表，并且它同时具有列表和矩阵的特性.

### 创建

`data.frame()`通过输入一系列向量来创建数据框,


```r
df <- data.frame(x = 1:3, y = c("a", "b", "c"))
str(df)
```

```
## 'data.frame':	3 obs. of  2 variables:
##  $ x: int  1 2 3
##  $ y: Factor w/ 3 levels "a","b","c": 1 2 3
```

显然，`data.frame()`默认把字符向量转化为因子，建议设置参数`stringAsFactors = FALSE`.

### 类型检测和转化

- `is.data.frame()`或者 `class()`测试其类型.
- `as.data.frame()`转化为数据框
    - 向量对象，转化为单列的数据库
    - 列表，列表的每一个元素转换为数据框的一列，因此要求列表元素长度必须相同，否则抛出错误
    - 矩阵，相同行列的数据库

### 合并

`rbind()`和`cbind()`用于合并数据库，`rbind()`要求数据框的列数和列名相同，`cbind()`要求行数相同，同时忽略行名.

**这两个函数是泛型函数，对于数据框的合并仅当至少有一个对象为数据框的时候才有意义，因为它们要求参数类型相同，会在合并之前把所有参数转化为数据框.**

### 特殊列

我们知道数据框是一系列向量构成的列表，因此它的每一列元素也可以是列表，如


```r
df <- data.frame(x = 1:3)
df$y <- list(1:2, 1:3, 1:4)
```

然而，利用`data.frame()`创建数据框的时候，如果参数为列表，会把列表的每一个元素作为数据框的一列. 如果要保持列表参数的原有数据结构，`I()`创建`AsIs`类来保持数据原有结构.


```r
dfl <- data.frame(x = 1:3, y = I(list(1:2, 1:3, 1:4)))
str(dfl)
```

```
## 'data.frame':	3 obs. of  2 variables:
##  $ x: int  1 2 3
##  $ y:List of 3
##   ..$ : int  1 2
##   ..$ : int  1 2 3
##   ..$ : int  1 2 3 4
##   ..- attr(*, "class")= chr "AsIs"
```

```r
dfl[3,"y"]
```

```
## [[1]]
## [1] 1 2 3 4
```

类似的，矩阵或者数组也可以作为数据框的元素(行数跟数据框中其他元素一致).
