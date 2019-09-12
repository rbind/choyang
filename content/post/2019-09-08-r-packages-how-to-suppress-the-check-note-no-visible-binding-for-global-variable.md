---
title: 'R packages: How to solve the check NOTE "no visible binding for global
  variable"'
author: ''
date: '2019-09-08'
slug: r-packages-how-to-solve-the-check-note-no-visible-binding-for-global-variable
categories: [R]
tags: [R, package-dev]
---

While our package employ a function using Non Standard Evaluation (NSE), such as [data.table](https://github.com/Rdatatable/data.table) and many [tidyverse](https://github.com/tidyverse/tidyverse) packages, R CMD check will generate NOTEs in the form "no visible binding for global variable xxx". There are two ways to solve this problem

First, add `utils::globalVariables(c("xxx"))` to your code, perhaps in `R/globals.R`. I recommand add it to the `R` file which caused the NOTE. Apprantly, `utils` packaage should be added to the Imports filed of `DESCRIPTION` file.

Second, as mentioned in the [vignette of dplyr](https://dplyr.tidyverse.org/articles/programming.html):

< If this function is in a package, using `.data` also prevents `R CMD check` from giving a NOTE about undefined global variables (provided that you’ve also imported `rlang::.data` with `@importFrom rlang .data`)

```
mutate_y <- function(df) {
  mutate(df, y = .data$a + .data$x)
}
```

