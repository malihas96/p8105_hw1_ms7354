Homework 1
================
Maliha Safdar (ms7354)
2025-09-18

``` r
library(moderndive)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
data("early_january_weather", package = "moderndive")
```

#### **Problem 1: Solution**

``` r
nrow(early_january_weather) # number of rows
```

    ## [1] 358

``` r
ncol(early_january_weather) # number of columns
```

    ## [1] 15

`In this first problem we will look at the behavior of the ggplot for different types of variables. The "early_january_weather" dataset has hourly meteorological data for LGA,JFK and EWR from January 2013. The size of the dataset is 358 rows and 15 columns. It has 15 variables and their names are:`

- origin

- year,month,day, hour, (for recording time)

- temp, dewp (that are measured in F)

- humid

- wind_dir, wind_speed, wind_gust (wind direction in degrees) and (gust
  speed in mph)

- precip (precipiitation, in inches)

- visib (in miles)

- time_hour (date and hour of the recording)\`

``` r
mean(early_january_weather$temp) # mean temperature
```

    ## [1] 39.58212

`The mean temperature is 39.58 F.`

##### Scatterplot for Temperature versus Time

``` r
ggplot(early_january_weather, aes(x=time_hour, y=temp, color = humid)) +
  geom_point()
```

![](Early_January_Weather_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggsave("scatter_plot.pdf", height = 4, width = 6)
```

`What I can observe from the scatterplot above is that as the temperature fluctuates between 40 degrees Farenheit to about 60 degrees Fareheit as time increases. The humidity can be seen to increase in the midpoint of Jan 7th and Jan 14th when the temperature is around 49 degrees Farenheit.`

#### **Problem 2: Solution**

`The sugar_df is a data frame that has information of amount of sugar in different fruits and the level of sugar each one has. It is a fictional dataframe I created so it is inaccurate.`

``` r
   vec_numeric = rnorm(10)
   vec_logical = vec_numeric > 0
   vec_char = c("apple","banana","cherry","dragonfruit","elderberry","fig","grapes","lychee","pineapple","mango")
     vec_factor = factor(c("high sugar level","high sugar level","medium sugar level","low sugar level","low sugar level","medium sugar level","medium sugar level","low sugar level","high sugar level","medium sugar level"))
```

``` r
sugar_df <- data.frame(
     sugar_amount = vec_numeric,
     sugar_grt_ten = vec_logical,
     fruit = vec_char,
     sugar_level = vec_factor
     )
```

``` r
(sugar_df)
```

    ##    sugar_amount sugar_grt_ten       fruit        sugar_level
    ## 1     0.6759191          TRUE       apple   high sugar level
    ## 2    -0.5483101         FALSE      banana   high sugar level
    ## 3     1.0439425          TRUE      cherry medium sugar level
    ## 4     0.5736256          TRUE dragonfruit    low sugar level
    ## 5    -1.3298822         FALSE  elderberry    low sugar level
    ## 6    -0.3151728         FALSE         fig medium sugar level
    ## 7    -0.1326591         FALSE      grapes medium sugar level
    ## 8    -1.4876842         FALSE      lychee    low sugar level
    ## 9    -1.3020255         FALSE   pineapple   high sugar level
    ## 10   -0.1943177         FALSE       mango medium sugar level

``` r
mean(sugar_df$sugar_amount) #mean for sugar_amount
```

    ## [1] -0.3016564

``` r
mean(sugar_df$sugar_grt_ten) #mean for sugar_grt_ten
```

    ## [1] 0.3

``` r
mean(sugar_df$fruit)        #mean for fruit
```

    ## Warning in mean.default(sugar_df$fruit): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
mean(sugar_df$sugar_level)  # mean for sugar_level
```

    ## Warning in mean.default(sugar_df$sugar_level): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

`When I took the mean of each variable I noticed that only the mean for sugar_amount (-0.38) and sugar_grt_0 (0.4) were populated. For the other two categorical variables no mean was populated.`

#### Using the pull function

`I pulled my variables from my sugar_df.`

``` r
pull(sugar_df,sugar_amount)
```

    ##  [1]  0.6759191 -0.5483101  1.0439425  0.5736256 -1.3298822 -0.3151728
    ##  [7] -0.1326591 -1.4876842 -1.3020255 -0.1943177

``` r
pull(sugar_df,sugar_grt_ten)
```

    ##  [1]  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
pull(sugar_df,fruit)
```

    ##  [1] "apple"       "banana"      "cherry"      "dragonfruit" "elderberry" 
    ##  [6] "fig"         "grapes"      "lychee"      "pineapple"   "mango"

``` r
pull(sugar_df,sugar_level)
```

    ##  [1] high sugar level   high sugar level   medium sugar level low sugar level   
    ##  [5] low sugar level    medium sugar level medium sugar level low sugar level   
    ##  [9] high sugar level   medium sugar level
    ## Levels: high sugar level low sugar level medium sugar level

#### Converting variables from one type to another using as.numeric

``` r
as.numeric(sugar_df$sugar_grt_ten)
```

``` r
as.numeric(sugar_df$fruit)
```

``` r
as.numeric(sugar_df$sugar_level)
```

`When I used the as.numeric function to convert the logical, character and factor to numeric variable it did convert it for logical and factor but it doesn't make sense to take a mean for those values. For example, the logical variable when converted to numeric becomes 0 and 1 and the mean for that wouldn't be the same as what was computed for the numeric variable. Likewise, when the factor was converted to numeric it only produced the levels 1,2 and 3. There was no numeric conversion observed for character variable.`
