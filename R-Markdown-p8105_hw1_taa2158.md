Homework 1 taa2158
================
Tanmayi Amanchi
2024-09-13

# Problem 1

First I will use the following code to load the penguins dataset

``` r
  data("penguins", package = "palmerpenguins")
```

The species of penguins in this dataset are Adelie from the Torgersen
island. There is information about their bill length (mm), bill depth
(mm), flipper length (mm), body mass (g), sex, and year.

Using the nrow and ncol function

``` r
  nrow(penguins)
```

    ## [1] 344

``` r
  ncol(penguins)
```

    ## [1] 8

There are 344 observations and 8 variables.

Using the Mean function and ommitting rows with NA in the calculation

``` r
  mean(na.omit(penguins[["flipper_length_mm"]]))
```

    ## [1] 200.9152

The mean flipper length is 200.9152

Now I will make a scatter plot of flipper_length_mm (y) vs
bill_length_mm (x); color points using the species variable. I’ve first
loaded the tidyverse package in order to create the scatter plot before
using the ggplot function. I will also save this plot as a jpeg using
the ggsave function. As noted in the warnings the rows containing
missing values or values outside the scale range were not included in
the plot.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) +
  geom_point() +
  labs(title = "Scatterplot of Flipper Length vs Bill Length",
       x = "Bill Length (mm)",
       y = "Flipper Length (mm)",
       color = "Species")
```

![](R-Markdown-p8105_hw1_taa2158_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggsave("scatterplot_flipper_vs_bill.jpeg")
```

    ## Saving 7 x 5 in image

# Problem 2

Create the data frame

``` r
penguin_q2 = tibble(
  sample_numeric = rnorm(10),                         
  sample_logical = rnorm(10) > 0,                      # Logical vector indicating if the sample is > 0
  sample_char = letters[1:10],                        # Character vector of length 10
  sample_factor = factor(sample(c("1", "2", "3"), 10, replace = TRUE))  # Factor vector with 3 levels
)

penguin_q2
```

    ## # A tibble: 10 × 4
    ##    sample_numeric sample_logical sample_char sample_factor
    ##             <dbl> <lgl>          <chr>       <fct>        
    ##  1         1.64   FALSE          a           2            
    ##  2        -0.550  TRUE           b           1            
    ##  3        -0.0624 TRUE           c           1            
    ##  4         0.750  TRUE           d           1            
    ##  5        -0.192  TRUE           e           1            
    ##  6         1.48   TRUE           f           3            
    ##  7         1.32   TRUE           g           2            
    ##  8         0.588  TRUE           h           1            
    ##  9        -0.389  TRUE           i           3            
    ## 10         0.0435 FALSE          j           2

Taking the mean of each variable in dataframe

``` r
means = tibble(
  sample_numeric_mean = mean(pull(penguin_q2, sample_numeric)),
  sample_logical_mean = mean(as.numeric(pull(penguin_q2, sample_logical))),
  sample_char_mean = mean(as.numeric(pull(penguin_q2, sample_char))),
  sample_factor_mean = mean(as.numeric(pull(penguin_q2, sample_factor))),
)
```

    ## Warning in mean(as.numeric(pull(penguin_q2, sample_char))): NAs introduced by
    ## coercion

The numeric variable gets coded as either close 1 or 0, which causes the
mean to be around 0.5. The logical variable is either TRUE or FALSE.
Meanwhile, the factor variable can get coded in regard to the levels of
1-3, thereby creating a mean close to 2. However, the character
variables get changed into NA’s by coercion, as there are no numeric
values, therefore a mean still cannot be calculate as the variables are
NA.
