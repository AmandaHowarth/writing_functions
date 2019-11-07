Writing\_functions
================
Amanda Howarth
11/7/2019

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ──────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(rvest)
```

    ## Loading required package: xml2

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     pluck

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
#code below just makes nice figures# 
knitr::opts_chunk$set(
    echo = TRUE, 
    warning = FALSE,
    fig.width = 8,
    fig.height = 6, 
    out.width = "90%"
)

options(
  ggplot2.continuous.color = "viridis", 
  ggplot2.continuous.fill = "viridis"
)

scale_colour_discrete = scale_colour_viridis_d
scale_fill_discrete = scale_fill_viridis_d

theme_set(theme_minimal() + theme(legend.position = "bottom"))
```

Writing functions\!

Here’s z scores

``` r
x = rnorm(n = 30, mean = 4, sd = 2.3)

x_again = rnorm(n = 30, mean =6, sd = 0.3)

y = rnorm(n = 30, mean = 4, sd = 2.3)


(x - mean(x)) / sd(x)
```

    ##  [1]  0.135544205  0.964152823 -2.291679528  0.569597130  0.601054059
    ##  [6] -0.347811338 -0.609439143  0.919165378 -1.336865981  2.140753602
    ## [11]  0.005065284  1.093264327  0.566964689 -0.234885328 -0.398850462
    ## [16] -0.667888874 -0.647504498  0.139011462 -0.631095105 -0.194707075
    ## [21]  1.158580504  0.541608831  1.471104954 -0.972285441 -0.995222493
    ## [26]  1.719111698 -0.989968016  0.120341528 -0.933418879 -0.893698314

``` r
(x_again - mean(x_again)) / sd(x_again)
```

    ##  [1] -0.68476233  1.14970169  0.78916676  0.68619499  1.76259529
    ##  [6]  1.84082755  0.79846439 -0.69804597  0.28870086 -1.68649029
    ## [11] -0.06679874 -2.05327858  0.73635703 -0.49518204  1.15638344
    ## [16] -0.45246130 -0.22325470  0.41239414  0.61183718  0.72015884
    ## [21] -1.00282473 -0.54022523 -0.97082648  1.01572779 -0.20732571
    ## [26] -0.56504864 -1.25700378  0.13645221 -1.58833966  0.38690603

``` r
# we would like to automate this process with functions so u don't have to keep writing over and over 
```

Now here’s a fucntion - u named it as an object (z\_score) updated to
add conditional statment - if X is not numeric (Character, etc.) and if
it is wrong it will output X should be numeric

``` r
z_score = function(x) {
  
  if(!is.numeric(x)) {
    stop("X should be numeric")
  } else if (length(x<3)) {
    stop("x should be longer than 3")
  }
  
  (x - mean(x)) / sd(x)
  
  
}
```

Try out the function you are making x as x\_again this time and it
ouputs (x - mean(x)) / sd(x) of x\_again using error = True lets u knit
even with errors

``` r
z_score(x = x_again)
```

    ## Error in z_score(x = x_again): x should be longer than 3

Examples of how the conditional statement works

``` r
z_score(x= 3) 
```

    ## Error in z_score(x = 3): x should be longer than 3

``` r
# NA
z_score(x= "my name is jeff")
```

    ## Error in z_score(x = "my name is jeff"): X should be numeric

## multiple outputs

here u want the mean & standard deviation of the x factor put it in a
tibble to make a dataframe

``` r
mean_and_sd = function(input_x) {
  
  if(!is.numeric(input_x)) {
    stop("X should be numeric")
  } else if (length(input_x<3)) {
    stop("x should be longer than 3")
  }
  tibble(
  mean_input = mean(input_x),
  sd_input = sd(input_x)
  )
    
}

#produces mean and standard deviation in a dataframe for whatever input the user out in
# could use a list instead (lists allow u to combine things and output many things)
```

testing above function

``` r
mean_and_sd(input_x = y)
```

    ## Error in mean_and_sd(input_x = y): x should be longer than 3
