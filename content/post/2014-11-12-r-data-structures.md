---
title: "R基础数据结构"
date: "2014-11-12"
tags: 
  - R
---


R中最基础，也是最重要的数据结构，可以根据其维度和元素的性质来划分：向量（原子向量和列表），矩阵、数组和数据框。<!--more-->

基本的数据结构根据维度和元素的性质(所有元素的类型是否相同)的可分为


|    | 同质          | 异质          |
|----|---------------|---------------|
| 1d | Atomic vector | List          |
| 2d | Matrix        | Data frame    |
| nd | Array         |               |


其他复杂的类型的数据都是基于以上类型构建的(OOP)，R中标量表示为长度为1的向量

了解一个对象的数据结构的构成最好的方法是利用函数`str`(structue的简写),显示对象的
内部结构

#### Vector

最基本的数据类型,表现为两种形式：原子向量(atomic
vector)和列表(list),区别就在于
元素的类型是否都一样，向量的三个基本特征为:

-   类型: `typeof`,其元素的类型
-   长度: `length`,元素个数
-   属性： `attributes`,额外的任意的元数据

**`is.vector`不是用来检测对象是否为向量,仅当向量除names属性外不含其他属性的时候
才会返回`TRUE`,`is.atomic(x) || is.list(x)`用于判断对象是否为向量**

此外,NULL作为保留字，代表了null对象，常用与表达式或者函数（未定义返回值)的返回值，
它同样是一个原子向量

    is.atomic(NULL)

    ## [1] TRUE

##### atomic vector

常见的原子向量有四种:logical,integer,double(常称为numeric),character,此外，使用较少的
有complex和raw两种

**NA是一个长度为1的逻辑向量,不同类型的向量中NA的类型也不同 NA\_real\_ (a
double vector), NA\_integer\_ and NA\_character\_,
在R都属于保留字(reserved words)**

##### 类型

`typeof`用来显示对象的类型，`is.*`可用来判定对象是否是某一特定类型（`is.character`,
`is.double`, `is.integer`, `is.logical`,`is.atomic`.

需要注意的是`is.numeric`当数据位integer或double时都返回TRUE

##### 原子向量元素的强制转化

每一个原子向量中元素的类型必须相同，当把不同类型的数据构成一个向量时，它们会被转化为最
灵活的类型，由低到高的顺序为logical, integer, double, and character

#### List

相比于`c`构建向量,list用`list`创建

    x <- list(1:3, "a", c(TRUE, FALSE, TRUE), c(2.3, 5.9))
    str(x)

    ## List of 4
    ##  $ : int [1:3] 1 2 3
    ##  $ : chr "a"
    ##  $ : logi [1:3] TRUE FALSE TRUE
    ##  $ : num [1:2] 2.3 5.9

list某些情况也可以称作**recursive**（递归）向量，因为list的元素也可以是list

    x <- list(list(list(list())))
    str(x)

    ## List of 1
    ##  $ :List of 1
    ##   ..$ :List of 1
    ##   .. ..$ : list()

    is.recursive(x)

    ## [1] TRUE

'c\`可以把多个list合并为一个

    x <- list(list(1, 2), c(3, 4))
    y <- c(list(1, 2), c(3, 4))
    x

    ## [[1]]
    ## [[1]][[1]]
    ## [1] 1
    ## 
    ## [[1]][[2]]
    ## [1] 2
    ## 
    ## 
    ## [[2]]
    ## [1] 3 4

    y

    ## [[1]]
    ## [1] 1
    ## 
    ## [[2]]
    ## [1] 2
    ## 
    ## [[3]]
    ## [1] 3
    ## 
    ## [[4]]
    ## [1] 4

`typeof`返回R内部对象的类型或者存储模式，对于列表它返回list，常用函数`is.list`,
`as.list`,`unlist`(转化为向量，数据会强制转化)，列表用于存储复杂的数据，比如df和
线性模型都是基于列表创建

#### attributes

任意对象都可包含额外属性来存储对象的元数据，属性可以看成命名的列表，当然不同属性
要求名字不同,`attr`提取特定名字的属性，`attributes`列出对象的所有属性。

    y <- 1:10
    attr(y, "my_attribute") <- "This is a vector"
    attr(y, "my_attribute")

    ## [1] "This is a vector"

    str(attributes(y))

    ## List of 1
    ##  $ my_attribute: chr "This is a vector"

`structure`也可以修改对象的属性

    structure(1:10, my_attribute = "This is a vector")

    ##  [1]  1  2  3  4  5  6  7  8  9 10
    ## attr(,"my_attribute")
    ## [1] "This is a vector"

当操作运算向量时，默认丢掉大部分附加属性。names，dim（一维的向量转为多维数组
或矩阵等和class(s3类)除外,当然这三 种属性一般不用`attr`改变。

    attributes(y[1])

    ## NULL

    attributes(sum(y))

    ## NULL

##### names

三种方法设定向量的names

-   `x <- c(a = 1, b = 2, c = 3)`
-   `x <- 1:3; names(x) <- c("a", "b", "c")`
-   `x <- setNames(1:3, c("a", "b", "c"))`

names不要求所有元素都是不同的，为了方便根据name提取向量子元素，name保持各不相同

#### factor

属性的一个最大用处是定义因子，levels就是作为因子默认存在的一个附加属性。因子可以看成是仅仅
包含预定义值（levels）的向量，用来存储分类数据。它是基于整型向量构建，附加了两个属性
class（factor）和levels，因子不可以合并(没有意义)

    c(factor("a"), factor("b"))

    ## [1] 1 1

当变量的可能取值已知时，即使并不知道一个数据集的所有取值。使用因子对于表示存在某些元素
并不含有观测值时更直观

    sex_char <- c("m", "m", "m")
    sex_factor <- factor(sex_char, levels = c("m", "f"))

    table(sex_char)

    ## sex_char
    ## m 
    ## 3

    table(sex_factor)

    ## sex_factor
    ## m f 
    ## 3 0

需要注意的是，当我们从文件读取数据定义一个数值型df时，如果数据中含有特殊字符（非数字)
如"."，“-”等，那么默认情况下这一列会转化为factor而不是数值型向量，可以通过先把它转化为
character类型向量然后再转化为数值型。更好的做法是在读入数据的时候设置`na.strings`。

此外，可以设置`stringsAsFactors = FALSE`,然后需要传话为factor时再转化，不要使用全局的选项
`options(stringsAsFactors = FALSE)`,改变全局设置，当与其他的包或者函数结合使用时，可能引起
不必要的麻烦。

虽然因子经常看起来像字符向量，实际上他们是以整型存储的，所以在对因子做字符处理的时候，可以先把
它转化为character，虽然某些函数可以自动转化因子为characte（`gsub()`
,`grepl`)，但是像 `nchar`,`c`等函数则会出现错误。

#### 矩阵-数组

通过设置原子向量的dim属性，可以构建多维数组、矩阵(2维数组)。`matrix`和`array`也用于构建矩阵和数组

    # Two scalar arguments to specify rows and columns
    a <- matrix(1:6, ncol = 3, nrow = 2)
    # One vector argument to describe all dimensions
    b <- array(1:12, c(2, 3, 2))

    # You can also modify an object in place by setting dim()
    c <- 1:6
    dim(c) <- c(3, 2,1)

常用函数

-   `nrow`,`ncol`，`dim`:行列数
-   `colnames`,`rolnames`:元素名称
-   `dimnames`:列表，对数组元素命名
-   `cbind`,`rbind`,`abind`:合并
-   `t`,`aperm`：转置
-   `is.*`,`as.*`

一维数组，矩阵和向量的区别,print可能相同，但是内部结构不同

    str(1:3)                   # 1d vector

    ##  int [1:3] 1 2 3

    str(matrix(1:3, ncol = 1)) # column vector

    ##  int [1:3, 1] 1 2 3

    str(matrix(1:3, nrow = 1)) # row vector

    ##  int [1, 1:3] 1 2 3

    str(array(1:3, 3))         # "array" vector

    ##  int [1:3(1d)] 1 2 3

此外，通过设置列表的dim属性，也可以把构建列表矩阵或者数组

#### df

df是R中最常用的存储数据的类型，使数据分析更容易。实际上，df一个列表（由多个相同
长度向量构成），同时具有列表和矩阵的属性。

    df <- data.frame(x = 1:3, y = c("a", "b", "c"))
    str(df)

    ## 'data.frame':    3 obs. of  2 variables:
    ##  $ x: int  1 2 3
    ##  $ y: Factor w/ 3 levels "a","b","c": 1 2 3

构建df时,默认情况下strings会转化为factors,通过参数`stringsAsFactors`控制。

df是一个s3类，它的类型(type)反应了构建df向量的类型：列表。

`as.data.frame`转化为df \* 向量：一列df \*
列表：每一个元素为一列，需要每一元素长度相等 \* 矩阵

##### 合并

-   `rbind`:要求列的names和length必须相同，`plyr::rbind.fill`可以用来合并含不同列的df
-   `cbind`：要求行的length必须相同,忽略rownames。作用于向量时会返回矩阵，除非某个参数是df

此外df是可以看成是一个向量列表，所以df的列也可以是一个列表

    df <- data.frame(x = 1:3)
    df$y <- list(1:2, 1:3, 1:4)
    df

    ##   x          y
    ## 1 1       1, 2
    ## 2 2    1, 2, 3
    ## 3 3 1, 2, 3, 4

然而，当利用`data.frame`构建df时，如果参数为list，它会把list的每一个元素作为df的一列

    ## error 要求list(y)中每个元素的长度与x相同
    data.frame(x = 1:3, y = list(1:2, 1:3, 1:4))

这是通过`I`可以保持原有参数的属性，时list保持一个整体作为df的一列，同样适用于矩阵和数组。

    dfl <- data.frame(x = 1:3, y = I(list(1:2, 1:3, 1:4)))
