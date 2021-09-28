homework 1
================
Huili Zheng
9/26/2021

## Problem 1

Create a data frame comprised of:

1.  a random sample of size 10 from a standard Normal distribution

2.  a logical vector indicating whether elements of the sample are
    greater than 0

3.  a character vector of length 10

4.  a factor vector of length 10, with 3 different factor “levels”

Try to take the mean of each variable in your data frame. What works and
what doesn’t?

``` r
 a = c(rnorm(10, mean = 0, sd = 1))
 b = a > 0
 c = c("Hello",",","This","is","Huili","Zheng",".","Thank","you","!")
 d = factor(c("low", "high", "medium", "high", "low", "medium", "high",  "low", "medium", "high"))
 
 answer1 <- tibble(a, b, c, d)
 
 mean(pull(answer1, a))
```

    ## [1] 0.05713492

``` r
 mean(pull(answer1, b))
```

    ## [1] 0.6

``` r
 mean(pull(answer1, c))
```

    ## Warning in mean.default(pull(answer1, c)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
 mean(pull(answer1, d))
```

    ## Warning in mean.default(pull(answer1, d)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

We can’t take the mean of the character and the factor vector. They are
not numerical or logical argument.

In some cases, you can explicitly convert variables from one type to
another. Write a code chunk that applies the as.numeric function to the
logical, character, and factor variables (please show this chunk but not
the output). What happens, and why? Does this help explain what happens
when you try to take the mean?

``` r
as.numeric(pull(answer1, b))
as.numeric(pull(answer1, c))
as.numeric(pull(answer1, d))
```

When we take the mean, we are manipulating the numerical value. The
logical variable can be transformed directly to 0 or 1. The factor
variable needs to be converted to numerical value then being taken the
mean. But the character can’t.

## Problem 2

Write a short description of the penguins dataset (not the penguins\_raw
dataset) using inline R code, including:

1.  the data in this dataset, including names / values of important
    variables
2.  the size of the dataset (using nrow and ncol)
3.  the mean flipper length
4.  Make a scatterplot of flipper\_length\_mm (y) vs bill\_length\_mm
    (x); color points using the species variable (adding color = …
    inside of aes in your ggplot code should help).

Export your first scatterplot to your project directory using ggsave.

``` r
data("penguins", package = "palmerpenguins")
describe(penguins)
```

    ## # A tibble: 8 × 8
    ##   variable          type     na na_pct unique    min   mean    max
    ##   <chr>             <chr> <int>  <dbl>  <int>  <dbl>  <dbl>  <dbl>
    ## 1 species           fct       0    0        3   NA     NA     NA  
    ## 2 island            fct       0    0        3   NA     NA     NA  
    ## 3 bill_length_mm    dbl       2    0.6    165   32.1   43.9   59.6
    ## 4 bill_depth_mm     dbl       2    0.6     81   13.1   17.2   21.5
    ## 5 flipper_length_mm int       2    0.6     56  172    201.   231  
    ## 6 body_mass_g       int       2    0.6     95 2700   4202.  6300  
    ## 7 sex               fct      11    3.2      3   NA     NA     NA  
    ## 8 year              int       0    0        3 2007   2008.  2009

``` r
names(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

``` r
size_sum(penguins)
```

    ## [1] "[344 × 8]"

``` r
data <- penguins %>% filter(flipper_length_mm > 0)
mean(pull(data,flipper_length_mm))
```

    ## [1] 200.9152

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](hw_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggsave("scatterplot with bill_length_mm and flipper_length_mm.jpg")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values (geom_point).

The dataset about penguins has 344 rows and 8 columns, including of
species, island, bill\_length\_mm, bill\_depth\_mm, flipper\_length\_mm,
body\_mass\_g, sex, year. There are missing values on species, island,
sex. The mean of flipper length is 200.9152 mm.
