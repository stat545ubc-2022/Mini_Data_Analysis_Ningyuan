Mini Data-Analysis Deliverable 1
================

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let’s get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr)
    package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

1.  Load the packages below.

<!-- -->

    library(datateachr)
    library(tidyverse)

    ## ── Attaching packages ────────────────────────────────── tidyverse 1.3.2 ──✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.2      ✔ forcats 0.5.2

    ## Warning: package 'readr' was built under R version 3.6.2

    ## Warning: package 'purrr' was built under R version 3.6.2

    ## ── Conflicts ───────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

    library(ggplot2)
    library(ggcorrplot)
    library(corrplot)

    ## corrplot 0.92 loaded

1.  Make a repository in the
    <a href="https://github.com/stat545ubc-2022" class="uri">https://github.com/stat545ubc-2022</a>
    Organization. You will be working with this repository for the
    entire data analysis project. You can either make it public, or make
    it private and add the TA’s and Lucy as collaborators.

# Instructions

## For Both Milestones

-   Each milestone is worth 45 points. The number of points allocated to
    each task will be annotated within each deliverable. Tasks that are
    more challenging will often be allocated more points.

-   10 points will be allocated to the reproducibility, cleanliness, and
    coherence of the overall analysis. While the two milestones will be
    submitted as independent deliverables, the analysis itself is a
    continuum - think of it as two chapters to a story. Each chapter, or
    in this case, portion of your analysis, should be easily followed
    through by someone unfamiliar with the content.
    [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/)
    is a good resource for what constitutes “good code”. Learning good
    coding practices early in your career will save you hassle later on!

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to the mini-analysis GitHub repository you made
earlier, and tag a release on GitHub. Then, submit a link to your tagged
release on canvas.

**Points**: This milestone is worth 45 points: 43 for your analysis, 1
point for having your Milestone 1 document knit error-free, and 1 point
for tagging your release on Github.

# Learning Objectives

By the end of this milestone, you should:

-   Become familiar with your dataset of choosing
-   Select 4 questions that you would like to answer with your data
-   Generate a reproducible and clear report using R Markdown
-   Become familiar with manipulating and summarizing your data in
    tibbles using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset (10 points)

The `datateachr` package by Hayley Boyce and Jordan Bourak currently
composed of 7 semi-tidy datasets for educational purposes. Here is a
brief description of each dataset:

-   *apt\_buildings*: Acquired courtesy of The City of Toronto’s Open
    Data Portal. It currently has 3455 rows and 37 columns.

-   *building\_permits*: Acquired courtesy of The City of Vancouver’s
    Open Data Portal. It currently has 20680 rows and 14 columns.

-   *cancer\_sample*: Acquired courtesy of UCI Machine Learning
    Repository. It currently has 569 rows and 32 columns.

-   *flow\_sample*: Acquired courtesy of The Government of Canada’s
    Historical Hydrometric Database. It currently has 218 rows and 7
    columns.

-   *parking\_meters*: Acquired courtesy of The City of Vancouver’s Open
    Data Portal. It currently has 10032 rows and 22 columns.

-   *steam\_games*: Acquired courtesy of Kaggle. It currently has 40833
    rows and 21 columns.

-   *vancouver\_trees*: Acquired courtesy of The City of Vancouver’s
    Open Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

-   We hope that this project will serve as practice for carrying our
    your own *independent* data analysis. Remember to comment your code,
    be explicit about what you are doing, and write notes in this
    markdown document when you feel that context is required. As you
    advance in the project, prompts and hints to do this will be
    diminished - it’ll be up to you!

-   Before choosing a dataset, you should always keep in mind **your
    goal**, or in other ways, *what you wish to achieve with this data*.
    This mini data-analysis project focuses on *data wrangling*,
    *tidying*, and *visualization*. In short, it’s a way for you to get
    your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 Out of the 7 datasets available in the `datateachr` package, choose
**4** that appeal to you based on their description. Write your choices
below:

**Note**: We encourage you to use the ones in the `datateachr` package,
but if you have a dataset that you’d really like to use, you can include
it here. But, please check with a member of the teaching team to see
whether the dataset is of appropriate complexity. Also, include a
**brief** description of the dataset here to help the teaching team
understand your data.

<!-------------------------- Start your work below ---------------------------->

Choice 1: cancer\_sample  
Choice 2: apt\_buildings  
Choice 3: parking\_meters  
Choice 4: flow\_sample

<!----------------------------------------------------------------------------->

1.2 One way to narrowing down your selection is to *explore* the
datasets. Use your knowledge of dplyr to find out at least *3*
attributes about each of these datasets (an attribute is something such
as number of rows, variables, class type…). The goal here is to have an
idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the
cleanliness of your analysis. I added a single code chunk for you below,
but do you want to use more than one? Would you like to write more
comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

    ### EXPLORE HERE ###
    datateachr::cancer_sample

    ## # A tibble: 569 × 32
    ##          ID diagn…¹ radiu…² textu…³ perim…⁴ area_…⁵ smoot…⁶ compa…⁷ conca…⁸
    ##       <dbl> <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M          18.0    10.4   123.    1001   0.118   0.278   0.300 
    ##  2   842517 M          20.6    17.8   133.    1326   0.0847  0.0786  0.0869
    ##  3 84300903 M          19.7    21.2   130     1203   0.110   0.160   0.197 
    ##  4 84348301 M          11.4    20.4    77.6    386.  0.142   0.284   0.241 
    ##  5 84358402 M          20.3    14.3   135.    1297   0.100   0.133   0.198 
    ##  6   843786 M          12.4    15.7    82.6    477.  0.128   0.17    0.158 
    ##  7   844359 M          18.2    20.0   120.    1040   0.0946  0.109   0.113 
    ##  8 84458202 M          13.7    20.8    90.2    578.  0.119   0.164   0.0937
    ##  9   844981 M          13      21.8    87.5    520.  0.127   0.193   0.186 
    ## 10 84501001 M          12.5    24.0    84.0    476.  0.119   0.240   0.227 
    ## # … with 559 more rows, 23 more variables: concave_points_mean <dbl>,
    ## #   symmetry_mean <dbl>, fractal_dimension_mean <dbl>, radius_se <dbl>,
    ## #   texture_se <dbl>, perimeter_se <dbl>, area_se <dbl>,
    ## #   smoothness_se <dbl>, compactness_se <dbl>, concavity_se <dbl>,
    ## #   concave_points_se <dbl>, symmetry_se <dbl>,
    ## #   fractal_dimension_se <dbl>, radius_worst <dbl>, texture_worst <dbl>,
    ## #   perimeter_worst <dbl>, area_worst <dbl>, smoothness_worst <dbl>, …

    #datateachr::apt_buildings
    #datateachr::parking_meters
    datateachr::flow_sample

    ## # A tibble: 218 × 7
    ##    station_id  year extreme_type month   day  flow sym  
    ##    <chr>      <dbl> <chr>        <dbl> <dbl> <dbl> <chr>
    ##  1 05BB001     1909 maximum          7     7   314 <NA> 
    ##  2 05BB001     1910 maximum          6    12   230 <NA> 
    ##  3 05BB001     1911 maximum          6    14   264 <NA> 
    ##  4 05BB001     1912 maximum          8    25   174 <NA> 
    ##  5 05BB001     1913 maximum          6    11   232 <NA> 
    ##  6 05BB001     1914 maximum          6    18   214 <NA> 
    ##  7 05BB001     1915 maximum          6    27   236 <NA> 
    ##  8 05BB001     1916 maximum          6    20   309 <NA> 
    ##  9 05BB001     1917 maximum          6    17   174 <NA> 
    ## 10 05BB001     1918 maximum          6    15   345 <NA> 
    ## # … with 208 more rows

<!----------------------------------------------------------------------------->

1.3 Now that you’ve explored the 4 datasets that you were initially most
interested in, let’s narrow it down to 2. What lead you to choose these
2? Briefly explain your choices below, and feel free to include any code
in your explanation.

<!-------------------------- Start your work below ---------------------------->

I decide to choose cancer\_sample and flow\_sample. I choose cancer
sample because it is more obvious than other datasets that it explores
how factors (radius mean, area mean, etc.) affect the diagnosis whether
a tumor is malicious or benign. I can then analysis and fit the data
using logistic regression because the response variable is binary. The
flow\_sample dataset is more like a time-series data, where I can
investigate the flow in different time and how does the flow changes
throughout the time. I can apply some time-series anlaysis techniques to
deal with the dataset. Thus, these two datasets are more familiar to me
and that is why I choose them.

<!----------------------------------------------------------------------------->

1.4 Time for the final decision! Going back to the beginning, it’s
important to have an *end goal* in mind. For example, if I had chosen
the `titanic` dataset for my project, I might’ve wanted to explore the
relationship between survival and other variables. Try to think of 1
research question that you would want to answer with each dataset. Note
them down below, and make your final choice based on what seems more
interesting to you!

<!-------------------------- Start your work below ---------------------------->

I finally decide to work on cancer\_sample dataset. In this dataset, I
want to explore the relationship between diagnosis of tumor (malicious
or benign) with other numeric explanatory variables, such as radius or
area mean. I am going to first start with exploratory analysis, feature
selection and then fit the data with logistic regression model.
Hopefully I can then understand which explanatory variables affect the
diagnosis of cancer !
<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them.
Probably also a good point to grab a coffee to get ready for the fun
part!

This project is semi-guided, but meant to be *independent*. For this
reason, you will complete tasks 2 and 3 below (under the **START HERE**
mark) as if you were writing your own exploratory data analysis report,
and this guidance never existed! Feel free to add a brief introduction
section to your project, format the document with markdown syntax as you
deem appropriate, and structure the analysis as you deem appropriate.
Remember, marks will be awarded for completion of the 4 tasks, but 10
points of the whole project are allocated to a reproducible and clean
analysis. If you feel lost, you can find a sample data analysis
[here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a
better idea. However, bear in mind that it is **just an example** and
you will not be required to have that level of complexity in your
project.

# Task 2: Exploring your dataset (15 points)

If we rewind and go back to the learning objectives, you’ll see that by
the end of this deliverable, you should have formulated *4* research
questions about your data that you may want to answer during your
project. However, it may be handy to do some more exploration on your
dataset of choice before creating these questions - by looking at the
data, you may get more ideas. **Before you start this task, read all
instructions carefully until you reach START HERE under Task 3**.

2.1 Complete *4 out of the following 8 exercises* to dive deeper into
your data. All datasets are different and therefore, not all of these
tasks may make sense for your data - which is why you should only answer
*4*. Use *dplyr* and *ggplot*.

1.  Plot the distribution of a numeric variable.
2.  Create a new variable based on other variables in your data (only if
    it makes sense)
3.  Investigate how many missing values there are per variable. Can you
    find a way to plot this?
4.  Explore the relationship between 2 variables in a plot.
5.  Filter observations in your data according to your own criteria.
    Think of what you’d like to explore - again, if this was the
    `titanic` dataset, I may want to narrow my search down to passengers
    born in a particular year…
6.  Use a boxplot to look at the frequency of different observations
    within a single variable. You can do this for more than one variable
    if you wish!
7.  Make a new tibble with a subset of your data, with variables and
    observations that you are interested in exploring.
8.  Use a density plot to explore any of your variables (that are
    suitable for this type of plot).

2.2 For each of the 4 exercises that you complete, provide a *brief
explanation* of why you chose that exercise in relation to your data (in
other words, why does it make sense to do that?), and sufficient
comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

    # read data, show summary
    cancer_sample <- as.tibble(datateachr::cancer_sample)

    ## Warning: `as.tibble()` was deprecated in tibble 2.0.0.
    ## Please use `as_tibble()` instead.
    ## The signature and semantics have changed, see `?as_tibble`.

    cancer_sample$diagnosis <- as.factor(cancer_sample$diagnosis)

    # Print the distributio of diagnosis (benign or malicious)
    ggplot(cancer_sample, aes(diagnosis, ..count..)) +
        geom_bar(fill = "lightblue", colour = 'black') 

![](mini-project-1_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

The first exploration is to examine the distribution of the response
variable, diagnosis. The reason I am doing this is to see whether the
dataset has imbalanced response variables or not. If the dataset is too
imbalanced, we might need to do some data transformation. After plot the
distribution, I see there are more cases of benign diagnosis than
malicious cases (a little imbalanced). However, the dataset is NOT
extremely imbalanced (the benign case is not way much larger than the
malicious case). So I do not have to do additional transformation for
the response variable.

    # Investigate how many missing values there are per variable
    any(is.na(cancer_sample))

    ## [1] FALSE

The second exploration is to check how many missing values there are in
the dataset. This check is important because if there are missing
values, we need to omit those entries during the exploration. After
checking, I find that there are zero (no) missing values in the dataset.
This is also good news since we do not need to do na.omit().

    # Plot the correlation matrix of the dataset
    corr_mat <- cor(cancer_sample[,3:ncol(cancer_sample)])
    corrplot(corr_mat)

![](mini-project-1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

    # Check the correlation between two variable, radius_mean and area_worst
    print(cor(cancer_sample$radius_mean, cancer_sample$area_worst))

    ## [1] 0.9410825

The third exploration is to create a correlation matrix between
explanatory variables. We want to do this in order to check the
collinearity in the dataset. From the correlation matrix, we can see
that there are many positive correlations between each pair of
explanatory variables. Besides, there are fewer negative correlations
between explanatory variables than postive correlations. For example,
radius\_mean and area\_worst have very high positive correlations, with
a corelation coefficient of 0.9410825.

    # Create two subsets, one where diagnosis is all B and the other where diagnosis is all M
    benign_subset <- filter(cancer_sample, diagnosis == "B")
    malicious_subset <- filter(cancer_sample, diagnosis == "M")

The fourth exploration is to subset the dataset based on the diagnosis
and then assign them into two new variables, benign\_subset and
malicious\_subset. I used filter function to create two subset where one
contains all benign cases, and the other all malicious cases. The reason
of doing this is that I can then analysis the data for each subset, for
example, to compute the mean or max of a variable for all malicious
tumors.

<!----------------------------------------------------------------------------->

# Task 3: Write your research questions (5 points)

So far, you have chosen a dataset and gotten familiar with it through
exploring the data. Now it’s time to figure out 4 research questions
that you would like to answer with your data! Write the 4 questions and
any additional comments at the end of this deliverable. These questions
are not necessarily set in stone - TAs will review them and give you
feedback; therefore, you may choose to pursue them as they are for the
rest of the project, or make modifications!

Question 1: How does each variable, such as radius\_mean, differ in the
case of malicious versus benign tumors ?  
Question 2: Are there any outliers in the dataset that we can remove to
make the distribution look better ?  
Question 3: Which subset of explanatory variables are significant in
affecting the diagnosis of tumors ? Which variables are insignificant
and can be eliminated (i.e. feature selection) ?  
Question 4: Are there any strong collinearity between the variables
(i.e. one explanatory variable with the other) ? How should we deal with
them in the data processing ?

# Task 4: Process and summarize your data (13 points)

From Task 2, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (10 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Based on two categorical variables, calculate two summary statistics
    of your choosing.

**Graphing:**

1.  Create a graph out of summarized variables that has at least two
    geom layers.
2.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
3.  Make a graph where it makes sense to customize the alpha
    transparency.
4.  Create 3 histograms out of summarized variables, with each histogram
    having different sized bins. Pick the “best” one and explain why it
    is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

    # For question 1: summarizing
    summary(malicious_subset$radius_mean)

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   10.95   15.07   17.32   17.46   19.59   28.11

    summary(benign_subset$radius_mean)

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   6.981  11.080  12.200  12.147  13.370  17.850

For research question 1, I look at all the malicious diagnosis examples.
I use the summary function to compute the range, mean, median, 25% and
75% quantile of the variable radius\_mean. The results are printed
above. We can then do the same thing for all the benign cases and
compare the mean, medium, and range in both cases, which are quite
useful in understanding the differences in their underlying
distributions. We can see that malicious tumors have higher mean radius
than benign tumors (also higher median, 25% and 75% quantiles).

    # For question 1: graphing
    ggplot(malicious_subset, aes(x= radius_mean)) +
                geom_histogram(bins=5)

![](mini-project-1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

    ggplot(malicious_subset, aes(x= radius_mean)) +
                geom_histogram(bins=10)

![](mini-project-1_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

    ggplot(malicious_subset, aes(x= radius_mean)) +
                geom_histogram(bins=20)

![](mini-project-1_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

For the graphing task, I plot the hist for radius\_mean in the malicious
subset, and choose the bin to be 5, 10 and 20 respectively. When
choosing the number of bins, there is a method called Sturge’s rule:
bins = 1 + ceil(log(n)). Using that formula, I get the expected number
of bins is 8.72792, which is close to 10. Therefore, I decide to choose
the second histogram where bin is 10. Choosing a proper bin is indeed
helpful because it can make the graph display nicer and show the pattern
in the data better.

    # For question 2: summarize
    cancer_sample$diagnosis <- as.factor(cancer_sample$diagnosis)
    summary(cancer_sample$diagnosis)

    ##   B   M 
    ## 357 212

For the second summarizing task, I compute the number of observations
for one categorical (also response) variable, which is diagnosis (a very
simple one). We can see there are 357 benign cases and 212 malicous
cases in diagnosis. Thus we know that the dataset is a little imbalanced
(more benign cases) but this imbalance is not serious enough to affect
our model fitting.

    # For question 2: graphing
    ggplot(data=cancer_sample, aes(x=diagnosis, y=area_se)) + geom_boxplot() + geom_count()

![](mini-project-1_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

In order to find outliers in the dataset, I need to look at the
distribution of each variable. I find the variable area\_se seems to
have a extremely large maximum value for the malicious diagnosis
Therefore, I create the plot above combining two geom layers,
geom\_boxplot and geom\_count. I find that there are two values in
malicious cases that are extremely larger than the median and mean
values. So these two entries can be outliers to remove from the data.

    # For question 3: summarizing
    radius_mean_level <- numeric()
    radius_mean_level[cancer_sample$radius_mean < 11] <- "low"
    radius_mean_level[cancer_sample$radius_mean >= 11 & cancer_sample$radius_mean < 13] <- "medium"
    radius_mean_level[cancer_sample$radius_mean >= 13 & cancer_sample$radius_mean < 15] <- "high"
    radius_mean_level[cancer_sample$radius_mean >= 15] <- "very high"
    radius_mean_level <- as.factor(radius_mean_level)

For question 3, I create a categorical variable with 4 groups from an
existing numerical variable, radius\_mean. Converting numeric variables
to categorical variables are useful because we can simplify continous
data into discrete. And we can then check the relationship between two
categorical variables, diagnosis and radius\_mean\_level. If we find
that malicious cases generally have more high and very high
radius\_mean\_level than benign cases, then we know they have positive
correlation.

    # For question 3: graphing
    cancer_sample$radius_mean_level <- radius_mean_level
    ggplot(cancer_sample, aes(x=factor(radius_mean_level, level = c("low", "medium", "high", "very high")), ..count.., alpha=..count..)) + geom_bar(aes(fill=diagnosis)) + labs(x = "radius_mean_level")

![](mini-project-1_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

I now create a graph showing how radius\_mean\_level is positively
correlated with the diagnosis. It is very easy to find that when the
radius mean level goes up from low to very high, the proportion of
counts that belongs to malicious diagnosis is greatly increased. Here I
add an alpha parameter where the transparencies of certain bars depends
on their respective counts. From this graph it is obvious that
radius\_mean\_level (also radius\_mean) is a significant explanatory
variable that affects the response variable which is diagnosis.

    # For question 4: summarizing
    summary(cancer_sample$diagnosis)

    ##   B   M 
    ## 357 212

    summary(cancer_sample$radius_mean_level)

    ##      high       low    medium very high 
    ##       139        85       171       174

    model <- glm(diagnosis ~ radius_mean_level, data = cancer_sample, family = binomial)
    summary(model)

    ## 
    ## Call:
    ## glm(formula = diagnosis ~ radius_mean_level, family = binomial, 
    ##     data = cancer_sample)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.2778  -0.3647  -0.1538   0.3941   2.9808  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                 -0.9416     0.1888  -4.988 6.11e-07 ***
    ## radius_mean_levellow        -3.4892     1.0235  -3.409 0.000652 ***
    ## radius_mean_levelmedium     -1.7357     0.3644  -4.763 1.91e-06 ***
    ## radius_mean_levelvery high   3.4581     0.3446  10.034  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 751.44  on 568  degrees of freedom
    ## Residual deviance: 349.96  on 565  degrees of freedom
    ## AIC: 357.96
    ## 
    ## Number of Fisher Scoring iterations: 7

For research question 4, I first calculate summary statistics of two
categorical variables, diagnosis and radius\_mean\_level. Then I try to
fit a simple logistic regression model to see how radius\_mean\_level
affects the response variable. In the model fitted, we see that the Pr
values for each level of radius\_mean\_level are smaller than 0.05,
suggesting that radius\_mean\_level is a significant variable affecting
diagnosis. The fitted model will also show summary statistics of
deviance residuals and coefficients for the model being fitted.

    # For question 4: graphing
    ggplot(data=cancer_sample, aes(x=radius_mean, y=area_mean)) +
      geom_line(linetype = "dashed", color = "blue") +
      geom_point(color = "red") +
      scale_y_continuous(trans = 'log2') + 
      labs(y = "log2(are_mean)")

![](mini-project-1_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

For research question 4, I find there are some collinearities between
individual explanatory variables. For example, the above plot shows that
there is a strong positive correlation (collinearity) between
radius\_mean and area\_mean. Moreover, I apply a log2 transformation of
the y-axis (area\_mean) and now the plot looks more nicer to be
presented and slightly more linear.

<!----------------------------------------------------------------------------->

### 1.2 (3 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!-------------------------- Start your work below ---------------------------->

I am about half closer to answering my research questions. I have
understood a lot about the dataset via the exploratory analysis. For
example, there are no missing values in the dataset and the response
variable is slightly imbalanced but acceptable. By plotting the
correlation matrix, I understand that most explanatory variales have
some positive correlation with the response variable, and some
collinearities exist. I believe all my research questions are yielding
interesting results. Maybe the second question (are there any outliers)
can be refined into saying: what kind of data transformation and
wrangling can we apply to make the data look better?

What remains unclear to me is that since there are so many explanatory
variables, I want to find a way that can help me perform feature
selections more quickly and easily instead of checking variables one by
one. There should be a R package that performs automatic feature
selections so I can use it directly. Also, I need to find a best model
to fit the data which includes all the explanatory variables. I am so
far unclear which model (logistic regression, SVM or random forest) fits
the data better.

<!----------------------------------------------------------------------------->

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and
Vincenzo Coia for launching.
