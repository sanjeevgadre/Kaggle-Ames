-   [Getting the Data](#getting-the-data)
-   [Introduction](#introduction)
-   [Random Forest Ensemble](#random-forest-ensemble)
-   [Boosted Tree Ensemble](#boosted-tree-ensemble)

Loading the required libraries.

    library(knitr)
    library(dplyr)
    library(ggplot2)
    library(randomForest)
    library(gbm)

### Getting the Data

1.  We start by getting the previously cleaned *train* subset.

### Introduction

1.  We will use the following 2 tree-based learning algorithms:
    1.  Random Forest Ensemble
    2.  Boosted Tree Ensemble
2.  We will use the *train-validate-test* strategy to fit an optimal
    model to the *train* data-set as well as estimate the likely test
    error.

### Random Forest Ensemble

1.  Since the *random forest* algorithm uses a *bootstrap* sampling
    strategy, the function `randomforest()` offers an easy built-in way
    to estimate test error without the need for an explicit *train-test*
    strategy.
2.  We iterate through different values of mumber of variables randomly
    sampled as candidates at each split allowing us to compare a random
    forest ensemble with a bagged tree ensemble in the same pass.
3.  For the two parameters to optimise we use the following sets
    1.  *number of trees grown* - {100, 500, 2500}, and
    2.  *number of features randomly chosen for a node split* - {p/9,
        p/3, p}, where is p is the number of features.
4.  (From the help file) For large data sets, especially those with
    large number of variables, calling randomForest via the formula
    interface is not advised: There may be too much overhead in handling
    the formula.

<!-- -->

    ## [1] "The estimated mean squared test error for a random forest ensemble model = 0.02"

    ## [1] "For the least mean squared test errror, the optimal number of trees grown is 1243 and the optimal number of parameters (for the model matrix) sampled at a node is 96"

*Observations*

1.  In this particular instance, the random forest ensemble outperforms
    the bagged tree ensemble.

### Boosted Tree Ensemble

1.  The function `gbm()` offers an in-built *n*-fold cross validation
    functionality that allows for an easy way to estimate test error
    without the need for an explicit *train-test* strategy.
2.  We iterate through a series of values for the parameters
    `interaction depth` and `learning rate` to identify the boosted tree
    ensemble model with the least estimated mean squared test error.
3.  For the two parameters to optimise we use the following sets
    1.  *interaction depth* - {1, 2, 3, 4}, and
    2.  *learning rate* - {1, 0.3, 0.1, 0.03, 0.1}

<!-- -->

    ## [1] "The estimated mean squared test error for a boosted forest ensemble model = 0.015"

    ## [1] "For the model with lowest mean squared test errror, the optimal interaction depth is 4 and the optimal learning rate is 0.01"

*Observations*

1.  While the *Random Forest Ensemble* does not outperform the penalised
    regression models, the *Boosted Tree Ensemble* certainly does.
