-   [Getting the Data](#getting-the-data)
-   [Introduction](#introduction)
-   [Principal Component Regression](#principal-component-regression)
-   [Partial Least Square Regression](#partial-least-square-regression)
-   [Best Subset Selection - Forward
    Selection](#best-subset-selection---forward-selection)
-   [Best Subset Selection - Backward
    Selection](#best-subset-selection---backward-selection)

Loading the required libraries.

    library(knitr)
    library(dplyr)
    library(pls)
    library(leaps)

### Getting the Data

1.  We start by getting the previously cleaned *train* subset.

<!-- -->

    train = readRDS("../RDA/train")

    n = nrow(train)
    p = ncol(train)-1
    y = train$SalePrice %>% log()

### Introduction

1.  We will use the following 3 learning algorithms that help reduce the
    dimensionality of the train data:
    1.  Principal Component Regression
    2.  Partial Least Square Regression
    3.  Regresion using the best subset.
2.  We will use the *train-validate-test* strategy to fit an optimal
    model to the *train* data-set as well as estimate the likely test
    error.
3.  The *PCR* and *PLS* algorithms work best when data is scaled.
    However the `pcr` and `plsr` functions are cumbersome to use with
    unscaled data especially when the data has features of different
    types. So it is best that we scale the data before using the
    algorigthm.
4.  Only the `numeric` features can be scaled. Additionally, there are
    some features that while `numeric` in type have range of values that
    make them more like `fct` featuers and scaling needs to be avoided
    for these features.
5.  We first identify the `numeric` features. We then use the *range* of
    these `numeric` features to identify features that are better
    treated as `fct` and then scale only the remaining `numeric`
    features.
6.  Since we use `log(SalePrice)` as our dependent variable we must
    scale `log(SalePrice)` and not `SalePrice`.

### Principal Component Regression

1.  We use the `pls` library's cross-validation function `crossval` for
    selection of optimal number of principal components and estimating
    the test error.

<!-- -->

    ## [1] "The estimated mean squared test error for a principal component regression model = 0.111"

    ## [1] "For the model with lowest mean squared test errror, the optimal number principal components =  78"

### Partial Least Square Regression

1.  We use the `pls` library's cross-validation function `crossval` for
    selection of optimal number of partial least square directions and
    estimating the test error.

<!-- -->

    ## [1] "The estimated mean squared test error for a partial least square regression model = 0.0587"

    ## [1] "For the model with lowest mean squared test errror, the optimal number partial least square directions =  78"

### Best Subset Selection - Forward Selection

1.  We perform a 10-fold cross validation to select the optimal size of
    the subset of features.
2.  The train data-set will be divided into 2 subsets - **train** and
    **test** - in the ratio 70:30. The *test subset* will be used to
    estimate the likely test error for a model buit using the optimal
    size of subset of features.

<!-- -->

    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:

    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:

    ## [1] "The estimated mean squared test error for a best subset (forward) selection model = 0.0295"

### Best Subset Selection - Backward Selection

1.  We use the same strategy as for the *Forward Selection* algorithm.

<!-- -->

    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:

    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:
    ## Reordering variables and trying again:

    ## [1] "The estimated mean squared test error for a best subset (backward) selection model = 0.0328"

*Observations* 1. None of the dimensionality reducing regression models
outperform the penalised regression models.
