p8105\_hw1\_CongyangXie
================
Congyang
9/25/2021

# Problem 1

-   Create a data frame comprised of:
    -   random sample of size 10 from a standard Normal distribution
    -   logical vector indicating whether elements of the sample are
        greater than 0
    -   a character vector of length 10
    -   factor vector of length 10, with 3 different factor “levels”

``` r
library(ggplot2)
library(schoolmath)

set.seed(1)
c1 = rnorm(10)
c2 = is.positive(c1)
c3 = rep_len('ImAChar', 10)
c4 = factor(sample(c("Lv1","Lv2","Lv3"), 10, replace = TRUE), ordered = TRUE, levels  = c("Lv1","Lv2","Lv3"))

df1 <- data.frame(c1, c2, c3, c4)
```

Try to take the mean of each variable in your dataframe. What works and
what doesn’t?

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1
    ## ✓ purrr   0.3.4

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
mean(pull(df1, 1))
```

    ## [1] 0.1322028

``` r
mean(pull(df1, 2))
```

    ## [1] 0.6

``` r
mean(pull(df1, 3))
```

    ## Warning in mean.default(pull(df1, 3)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
mean(pull(df1, 4))
```

    ## Warning in mean.default(pull(df1, 4)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

The first mean is simply the arithmetic average. The true is 1, false is
0. But the third and last ones are not numeric or logical data, so their
mean cannot be calculated.

``` r
mean(as.numeric(pull(df1,2)))
mean(as.numeric(pull(df1,3)))
```

    ## Warning in mean(as.numeric(pull(df1, 3))): NAs introduced by coercion

``` r
mean(as.numeric(pull(df1,4)))
```

When using as.numeric(), it turns characters in column 3 to NAs and 3
ordinal factors in column 4 to 1, 2, 3.

# Problem 2

-   Write a short description of the penguins dataset (not the
    penguins\_raw dataset) using inline R code, including:

    -   the data in this dataset, including names / values of important
        variables
    -   the size of the dataset (using nrow and ncol)
    -   the mean flipper length

``` r
data("penguins", package = "palmerpenguins")
```

-   The variables in the penguins are: species, island,
    bill\_length\_mm, bill\_depth\_mm, flipper\_length\_mm,
    body\_mass\_g, sex, year.
-   The peguines dataset has 344 rows and 8 columns.
-   “species” is a factor variable, which has unique values: Adelie,
    Chinstrap, Gentoo.
-   “island” is a factor variable, which has unique values: Biscoe,
    Dream, Torgersen.
-   “sex” is a factor variable, which has unique values: female, male.
-   “bill\_length\_mm” is a numeric variable, whose mean is 43.9219298,
    median is 44.45, standard deviation is 5.4595837, range is 27.5.
-   “bill\_depth\_mm” is a numeric variable, whose mean is 17.1511696,
    median is 17.3, standard deviation is 1.9747932, and range is 8.4.
-   “flipper\_length\_mm” is a numeric variable, whose mean is
    200.9152047, median is 197, standard deviation is 14.0617137, and
    range is 59.
-   “body\_mass\_g” is a numeric variable, whose mean is 4201.754386,
    median is 4050, standard deviation is 801.9545357, and range
    is 3600.
-   “year” has unique values: 2007, 2008, 2009.
-   The mean flipper length is 200.9152047.
