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

    ## [1] -0.009037543

``` r
mean(pull(df1, 2))
```

    ## [1] 0.5

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
stat_penguins_raw <- skimr::skim(penguins_raw)
#pull(stat_penguins_raw, "skim_variable")
#list(t(stat_penguins_raw[stat_penguins_raw$skim_type == "character", 2]))
count(unique(penguins_raw[,1]))
```

    ## # A tibble: 1 × 1
    ##       n
    ##   <int>
    ## 1     3

The variables in the penguins\_raw are: studyName, Species, Region,
Island, Stage, Individual ID, Clutch Completion, Sex, Comments, Date
Egg, Sample Number, Culmen Length (mm), Culmen Depth (mm), Flipper
Length (mm), Body Mass (g), Delta 15 N (o/oo), Delta 13 C (o/oo). The
peguines\_raw dataset has 344 rows and 17 columns. studyName has unique
values
