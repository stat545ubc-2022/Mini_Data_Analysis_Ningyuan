Mini Data Analysis Milestone 2
================

*To complete this milestone, you can edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to your second (and last) milestone in your mini data analysis project!

In Milestone 1, you explored your data, came up with research questions,
and obtained some results by making summary tables and graphs. This
time, we will first explore more in depth the concept of *tidy data.*
Then, you’ll be sharpening some of the results you obtained from your
previous milestone by:

- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 55 points (compared to the 45 points
of the Milestone 1): 45 for your analysis, and 10 for your entire
mini-analysis GitHub repository. Details follow.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

- Understand what *tidy* data is, and how to create it using `tidyr`.
- Generate a reproducible and clear report using R Markdown.
- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) # <- might contain the data you picked!
library(tidyverse)
library(ggplot2)
library(ggcorrplot)
library(corrplot)
library(forcats)
library(broom)
```

``` r
cancer_sample <- as_tibble(datateachr::cancer_sample)
cancer_sample$diagnosis <- as.factor(cancer_sample$diagnosis)
cancer_sample_subset <- cancer_sample[, 1:8]
```

# Task 1: Tidy your data (15 points)

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

- Each row is an **observation**
- Each column is a **variable**
- Each cell is a **value**

*Tidy’ing* data is sometimes necessary because it can simplify
computation. Other times it can be nice to organize data so that it can
be easier to understand when read manually.

### 2.1 (2.5 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

I choose the cancer_sample dataset, since there are more than 8
variables I pick the first eight variables as a subset to answer this
question.

The data is tidy, because each row is an observation; each column is a
variable; each cell is a value.
<!----------------------------------------------------------------------------->

### 2.2 (5 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

``` r
# untidy data
cancer_sample_subset_untidy <- cancer_sample_subset %>% 
                pivot_wider(names_from = diagnosis,
                            values_from = radius_mean)
print(cancer_sample_subset_untidy)
```

    ## # A tibble: 569 × 8
    ##          ID texture_mean perimeter_mean area_mean smoothne…¹ compa…²     M     B
    ##       <dbl>        <dbl>          <dbl>     <dbl>      <dbl>   <dbl> <dbl> <dbl>
    ##  1   842302         10.4          123.      1001      0.118   0.278   18.0    NA
    ##  2   842517         17.8          133.      1326      0.0847  0.0786  20.6    NA
    ##  3 84300903         21.2          130       1203      0.110   0.160   19.7    NA
    ##  4 84348301         20.4           77.6      386.     0.142   0.284   11.4    NA
    ##  5 84358402         14.3          135.      1297      0.100   0.133   20.3    NA
    ##  6   843786         15.7           82.6      477.     0.128   0.17    12.4    NA
    ##  7   844359         20.0          120.      1040      0.0946  0.109   18.2    NA
    ##  8 84458202         20.8           90.2      578.     0.119   0.164   13.7    NA
    ##  9   844981         21.8           87.5      520.     0.127   0.193   13      NA
    ## 10 84501001         24.0           84.0      476.     0.119   0.240   12.5    NA
    ## # … with 559 more rows, and abbreviated variable names ¹​smoothness_mean,
    ## #   ²​compactness_mean

``` r
# Convert untidy back to tidy
cancer_sample_subset_tidy <- cancer_sample_subset_untidy %>% 
                pivot_longer(cols = c(M, B),
                            names_to = "diagnosis", 
                            values_to = "radius_mean",
                            values_drop_na = TRUE) %>%
                select(ID, diagnosis, radius_mean, everything()) 
print(cancer_sample_subset_tidy)
```

    ## # A tibble: 569 × 8
    ##          ID diagnosis radius_mean texture_mean perimet…¹ area_…² smoot…³ compa…⁴
    ##       <dbl> <chr>           <dbl>        <dbl>     <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M                18.0         10.4     123.    1001   0.118   0.278 
    ##  2   842517 M                20.6         17.8     133.    1326   0.0847  0.0786
    ##  3 84300903 M                19.7         21.2     130     1203   0.110   0.160 
    ##  4 84348301 M                11.4         20.4      77.6    386.  0.142   0.284 
    ##  5 84358402 M                20.3         14.3     135.    1297   0.100   0.133 
    ##  6   843786 M                12.4         15.7      82.6    477.  0.128   0.17  
    ##  7   844359 M                18.2         20.0     120.    1040   0.0946  0.109 
    ##  8 84458202 M                13.7         20.8      90.2    578.  0.119   0.164 
    ##  9   844981 M                13           21.8      87.5    520.  0.127   0.193 
    ## 10 84501001 M                12.5         24.0      84.0    476.  0.119   0.240 
    ## # … with 559 more rows, and abbreviated variable names ¹​perimeter_mean,
    ## #   ²​area_mean, ³​smoothness_mean, ⁴​compactness_mean

I first change the tidy data to untidy one using pivot_wider() function
and name it cancer_sample_subset_untidy. The data become untidy because
the last two columns are not variables, so it does not statisfy the
requirement where each column must be a variable. Then I convert the
untidy data back to tidy one using pivot_longer() function, and reorder
the columns using select() and everything() to make it the same as the
original data.

<!----------------------------------------------------------------------------->

### 2.3 (7.5 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the next four tasks:

<!-------------------------- Start your work below ---------------------------->

1.  For malicious diagnosis, which feature has the highest average
    standard error and what is that largest value ?
2.  How does the average area_worst in benign cases compare with the
    avarege area_mean in malicious cases and what is their difference ?

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

In my previous milestone, I have chosen a set of research questions more
related to feature selection and regression. And I did not focus on the
meaning of each variable too much in detail. Therefore, in this task, I
decide to do more explanatory data analysis, using the data manipulation
functions (filter, cleaning, and etc.). To be more specific, for
question 1, I want to learn about which of the ten features (radius,
texture, and etc.) tend to have the highest mean standard error in
malicious tumors. This is important because then I know which feature in
malicious dianosis has the highest variability. In my second question, I
want to know how the average area_worst in benign cases compare with
average area_mean in malicious cases, and their difference. I want to
ensure that even the average area_worst in benign tumors is smaller than
the average area_mean in the malicious tumors.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

<!--------------------------- Start your work below --------------------------->

``` r
# Question 1, find the feature with higest average se
average_se_for_all_cols <- cancer_sample %>% 
                filter(diagnosis == "M") %>%
                select(ends_with("se")) %>%
                summarise_if(is.numeric, mean)
highest_se <- average_se_for_all_cols[which.max(average_se_for_all_cols)]
print(highest_se)
```

    ## # A tibble: 1 × 1
    ##   area_se
    ##     <dbl>
    ## 1    72.7

For question 1, we find that for malicious tumors, area_se has the
highest standard error and the value is 72.67241.

``` r
# Question 2, find diff between average area_mean in malicious and average area_worst in benign
temp_subset_q2 <- (cancer_sample %>% 
    group_by(diagnosis) %>%
    summarise_all(.funs = c(mean="mean")) %>%
    select(diagnosis, area_worst_mean, area_mean_mean)) 
print(temp_subset_q2)
```

    ## # A tibble: 2 × 3
    ##   diagnosis area_worst_mean area_mean_mean
    ##   <fct>               <dbl>          <dbl>
    ## 1 B                    559.           463.
    ## 2 M                   1422.           978.

``` r
area_diff <- temp_subset_q2[[2, 3]] - temp_subset_q2[[1, 2]]
print(area_diff)
```

    ## [1] 419.477

We can see that the average area_mean in malicious tumors is even larger
than the average area_worst in benign tumors, and the difference is
419.477.

<!----------------------------------------------------------------------------->

# Task 2: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

<!-------------------------- Start your work below ---------------------------->

``` r
# Create a categorical variable with > 3 groups
radius_mean_level <- numeric()
radius_mean_level[cancer_sample$radius_mean < 11] <- "low"
radius_mean_level[cancer_sample$radius_mean >= 11 & cancer_sample$radius_mean < 13] <- "medium"
radius_mean_level[cancer_sample$radius_mean >= 13 & cancer_sample$radius_mean < 21] <- "high"
radius_mean_level[cancer_sample$radius_mean >= 21] <- "very high"
radius_mean_level <- as.factor(radius_mean_level)

# use ggplot to plot
cancer_sample$radius_mean_level <- radius_mean_level
ggplot(cancer_sample, aes(x=radius_mean_level, ..count..)) + 
    geom_bar(aes(fill=diagnosis)) + labs(x = "radius_mean_level")
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)

        - Note that you might first have to *make* a time-based column
          using a function like `ymd()`, but this doesn’t count.
        - Examples of something you might do here: extract the day of
          the year from a date, or extract the weekday, or let 24 hours
          elapse on your dates.

    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).

        - For example, you could say something like “Investigating the
          day of the week might be insightful because penguins don’t
          work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number**: 1

``` r
ggplot(cancer_sample, aes(x=fct_reorder(radius_mean_level, radius_mean), ..count..)) +
    geom_bar(aes(fill=diagnosis)) + labs(x = "radius_mean_level")
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

In my original plot, the radius_mean_level is ordered by high, low,
medium, and very high, which is the alphabetical order of the first
letter. However, this is not the order we want it to be. We want the
order to be from low, medium, high to very high (i.e. based on the
radius_mean value from small to large). Therefore, we apply the
fct_reorder() function, which is going to reorder the radius_mean_level
based on the values of radius_mean in an ascending order After applying
the function, we can see the radius_mean_level is reordered to become
low, medium, high and very high, which is expected.

<!----------------------------------------------------------------------------->
<!-------------------------- Start your work below ---------------------------->

**Task Number**: 2

``` r
ggplot(cancer_sample, aes(x=fct_collapse(radius_mean_level, high = c("high", "very high")), ..count..)) +
    geom_bar(aes(fill=diagnosis)) + labs(x = "radius_mean_level")
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

From the orginal plot, we see there are only few observations in very
high level. So we can merge high and very high levels into one single
level called high. We can use fct_collapse() function to collapse factor
levels into manually defined groups.

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: What are the effects of the 30 explanatory
variables on the response variable diagnosis. Can we fit a model to
examine the relationship ?

**Variable of interest**: diagnosis

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

- **Note**: It’s OK if you don’t know how these models/tests work. Here
  are some examples of things you can do here, but the sky’s the limit.

  - You could fit a model that makes predictions on Y using another
    variable, by using the `lm()` function.
  - You could test whether the mean of Y equals 0 using `t.test()`, or
    maybe the mean across two groups are different using `t.test()`, or
    maybe the mean across multiple groups are different using `anova()`
    (you may have to pivot your data for the latter two).
  - You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

``` r
model <- glm(diagnosis ~ .-ID-radius_mean_level, data = cancer_sample, family = binomial)
```

    ## Warning: glm.fit: algorithm did not converge

    ## Warning: glm.fit: fitted probabilities numerically 0 or 1 occurred

``` r
summary(model)
```

    ## 
    ## Call:
    ## glm(formula = diagnosis ~ . - ID - radius_mean_level, family = binomial, 
    ##     data = cancer_sample)
    ## 
    ## Deviance Residuals: 
    ##    Min      1Q  Median      3Q     Max  
    ##  -8.49   -8.49   -8.49    8.49    8.49  
    ## 
    ## Coefficients:
    ##                           Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)             -2.881e+06  2.816e+05 -10.233  < 2e-16 ***
    ## radius_mean              2.427e+06  2.693e+05   9.014  < 2e-16 ***
    ## texture_mean             1.958e+05  1.471e+04  13.313  < 2e-16 ***
    ## perimeter_mean           1.473e+06  2.464e+04  59.791  < 2e-16 ***
    ## area_mean               -1.301e+05  3.907e+03 -33.301  < 2e-16 ***
    ## smoothness_mean         -1.525e+08  8.361e+06 -18.234  < 2e-16 ***
    ## compactness_mean        -6.428e+06  3.213e+06  -2.001  0.04539 *  
    ## concavity_mean           1.042e+06  1.408e+06   0.740  0.45959    
    ## concave_points_mean     -1.716e+07  5.382e+06  -3.188  0.00143 ** 
    ## symmetry_mean            4.049e+07  7.772e+05  52.093  < 2e-16 ***
    ## fractal_dimension_mean  -4.233e+07  2.169e+06 -19.519  < 2e-16 ***
    ## radius_se                3.328e+07  1.169e+06  28.478  < 2e-16 ***
    ## texture_se               6.368e+06  2.005e+05  31.763  < 2e-16 ***
    ## perimeter_se             1.701e+06  4.720e+04  36.032  < 2e-16 ***
    ## area_se                 -6.393e+05  1.835e+04 -34.840  < 2e-16 ***
    ## smoothness_se            7.492e+08  1.224e+07  61.213  < 2e-16 ***
    ## compactness_se          -1.773e+08  5.732e+06 -30.931  < 2e-16 ***
    ## concavity_se             1.529e+08  5.340e+06  28.624  < 2e-16 ***
    ## concave_points_se       -1.260e+09  4.012e+07 -31.398  < 2e-16 ***
    ## symmetry_se              2.890e+08  4.126e+06  70.055  < 2e-16 ***
    ## fractal_dimension_se     1.512e+09  6.597e+07  22.921  < 2e-16 ***
    ## radius_worst            -6.130e+06  2.143e+05 -28.606  < 2e-16 ***
    ## texture_worst           -5.832e+05  2.437e+04 -23.935  < 2e-16 ***
    ## perimeter_worst         -3.538e+05  1.219e+04 -29.023  < 2e-16 ***
    ## area_worst               8.950e+04  2.741e+03  32.658  < 2e-16 ***
    ## smoothness_worst        -2.161e+07  3.298e+06  -6.553 5.65e-11 ***
    ## compactness_worst        8.986e+06  3.999e+05  22.470  < 2e-16 ***
    ## concavity_worst         -3.028e+07  1.523e+06 -19.876  < 2e-16 ***
    ## concave_points_worst     1.431e+08  5.471e+06  26.162  < 2e-16 ***
    ## symmetry_worst          -2.474e+07  3.392e+05 -72.923  < 2e-16 ***
    ## fractal_dimension_worst -3.698e+07  5.340e+06  -6.926 4.32e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance:   751.44  on 568  degrees of freedom
    ## Residual deviance: 32006.76  on 538  degrees of freedom
    ## AIC: 32069
    ## 
    ## Number of Fisher Scoring iterations: 25

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

- Be sure to indicate in writing what you chose to produce.
- Your code should either output a tibble (in which case you should
  indicate the column that contains the thing you’re looking for), or
  the thing you’re looking for itself.
- Obtain your results using the `broom` package if possible. If your
  model is not compatible with the broom function you’re needing, then
  you can obtain your results by some other means, but first indicate
  which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

``` r
# obtain a tibble to summary the model output
tidy_model_summary <- tidy(model)
print(tidy_model_summary)
```

    ## # A tibble: 31 × 5
    ##    term                   estimate std.error statistic   p.value
    ##    <chr>                     <dbl>     <dbl>     <dbl>     <dbl>
    ##  1 (Intercept)           -2881303.   281571.   -10.2   1.41e- 24
    ##  2 radius_mean            2427012.   269257.     9.01  1.99e- 19
    ##  3 texture_mean            195783.    14706.    13.3   1.94e- 40
    ##  4 perimeter_mean         1473188.    24639.    59.8   0        
    ##  5 area_mean              -130118.     3907.   -33.3   3.70e-243
    ##  6 smoothness_mean     -152452198.  8360682.   -18.2   2.75e- 74
    ##  7 compactness_mean      -6428386.  3212621.    -2.00  4.54e-  2
    ##  8 concavity_mean         1041553.  1408411.     0.740 4.60e-  1
    ##  9 concave_points_mean  -17156858.  5381835.    -3.19  1.43e-  3
    ## 10 symmetry_mean         40485923.   777187.    52.1   0        
    ## # … with 21 more rows

``` r
pval_area_mean <- tidy_model_summary %>%
                        filter(term == "area_mean") %>%
                        select(p.value) 
print(pval_area_mean)
```

    ## # A tibble: 1 × 1
    ##     p.value
    ##       <dbl>
    ## 1 3.70e-243

I first use broom package tidy() function to convert the model into a
tibble. Then I produce the p-value for the term area_mean and store it
into a new variable tibble called pval_area_mean, as above. The p-value
for area_mean is 3.697154e-243.

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 1 (Task 4.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

- **Robustness criteria**: You should be able to move your Mini Project
  repository / project folder to some other location on your computer,
  or move this very Rmd file to another location within your project
  repository / folder, and your code should still work.
- **Reproducibility criteria**: You should be able to delete the csv
  file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

``` r
# write table as dataframe to output folder
summary_table <- data.frame(summary(cancer_sample))
path_table <- paste(here::here(), "Output/table.csv",sep = "/")
write_csv(summary_table, path_table)
```

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

- The same robustness and reproducibility criteria as in 3.1 apply here.

<!-------------------------- Start your work below ---------------------------->

``` r
path_model <- paste(here::here(), "Output/model.rds",sep = "/")
# save the model
saveRDS(model, path_model)
# load the model
model2 <- readRDS(path_model)
summary(model2)
```

    ## 
    ## Call:
    ## glm(formula = diagnosis ~ . - ID - radius_mean_level, family = binomial, 
    ##     data = cancer_sample)
    ## 
    ## Deviance Residuals: 
    ##    Min      1Q  Median      3Q     Max  
    ##  -8.49   -8.49   -8.49    8.49    8.49  
    ## 
    ## Coefficients:
    ##                           Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)             -2.881e+06  2.816e+05 -10.233  < 2e-16 ***
    ## radius_mean              2.427e+06  2.693e+05   9.014  < 2e-16 ***
    ## texture_mean             1.958e+05  1.471e+04  13.313  < 2e-16 ***
    ## perimeter_mean           1.473e+06  2.464e+04  59.791  < 2e-16 ***
    ## area_mean               -1.301e+05  3.907e+03 -33.301  < 2e-16 ***
    ## smoothness_mean         -1.525e+08  8.361e+06 -18.234  < 2e-16 ***
    ## compactness_mean        -6.428e+06  3.213e+06  -2.001  0.04539 *  
    ## concavity_mean           1.042e+06  1.408e+06   0.740  0.45959    
    ## concave_points_mean     -1.716e+07  5.382e+06  -3.188  0.00143 ** 
    ## symmetry_mean            4.049e+07  7.772e+05  52.093  < 2e-16 ***
    ## fractal_dimension_mean  -4.233e+07  2.169e+06 -19.519  < 2e-16 ***
    ## radius_se                3.328e+07  1.169e+06  28.478  < 2e-16 ***
    ## texture_se               6.368e+06  2.005e+05  31.763  < 2e-16 ***
    ## perimeter_se             1.701e+06  4.720e+04  36.032  < 2e-16 ***
    ## area_se                 -6.393e+05  1.835e+04 -34.840  < 2e-16 ***
    ## smoothness_se            7.492e+08  1.224e+07  61.213  < 2e-16 ***
    ## compactness_se          -1.773e+08  5.732e+06 -30.931  < 2e-16 ***
    ## concavity_se             1.529e+08  5.340e+06  28.624  < 2e-16 ***
    ## concave_points_se       -1.260e+09  4.012e+07 -31.398  < 2e-16 ***
    ## symmetry_se              2.890e+08  4.126e+06  70.055  < 2e-16 ***
    ## fractal_dimension_se     1.512e+09  6.597e+07  22.921  < 2e-16 ***
    ## radius_worst            -6.130e+06  2.143e+05 -28.606  < 2e-16 ***
    ## texture_worst           -5.832e+05  2.437e+04 -23.935  < 2e-16 ***
    ## perimeter_worst         -3.538e+05  1.219e+04 -29.023  < 2e-16 ***
    ## area_worst               8.950e+04  2.741e+03  32.658  < 2e-16 ***
    ## smoothness_worst        -2.161e+07  3.298e+06  -6.553 5.65e-11 ***
    ## compactness_worst        8.986e+06  3.999e+05  22.470  < 2e-16 ***
    ## concavity_worst         -3.028e+07  1.523e+06 -19.876  < 2e-16 ***
    ## concave_points_worst     1.431e+08  5.471e+06  26.162  < 2e-16 ***
    ## symmetry_worst          -2.474e+07  3.392e+05 -72.923  < 2e-16 ***
    ## fractal_dimension_worst -3.698e+07  5.340e+06  -6.926 4.32e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance:   751.44  on 568  degrees of freedom
    ## Residual deviance: 32006.76  on 538  degrees of freedom
    ## AIC: 32069
    ## 
    ## Number of Fisher Scoring iterations: 25

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least four folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

- All Rmd files have been `knit`ted to their output, and all data files
  saved from Task 4 above appear in the `output` folder.
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 1 document knits error-free, and the Milestone 2 document
knits error-free.

## Tagged release (1 point)

You’ve tagged a release for Milestone 1, and you’ve tagged a release for
Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
