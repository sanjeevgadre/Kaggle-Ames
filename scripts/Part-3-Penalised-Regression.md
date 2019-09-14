-   [Getting the Data](#getting-the-data)
-   [Introduction](#introduction)
-   [Unpenalised Linear Regression](#unpenalised-linear-regression)
-   [Ridge Penalised Linear
    Regression](#ridge-penalised-linear-regression)
-   [Lasso Penalised Linear
    Regression](#lasso-penalised-linear-regression)

Loading the required libraries.

### Getting the Data

1.  We start by getting the previously cleaned *train* subset.

<!-- -->

    train = readRDS("../RDA/train")

### Introduction

1.  We will build both the ridge penalised and lasso penalised
    regression models.
2.  The `glmnet` package offers the `cv.glmnet()` function which allows
    a simple method to perform a n-fold cross validation to estimate the
    mean squared test error.
3.  We first establish a baseline by estimating the likely test error
    for an un-penalised linear regresssion model.

<!-- -->

    n = nrow(train)
    p = ncol(train) - 1
    y = train$SalePrice %>% log()
    x = model.matrix(SalePrice~., data = train)[,-1]

### Unpenalised Linear Regression

    ## [1] "The estimated mean squared test error for a un penalised linear regression model = 0.0207"

### Ridge Penalised Linear Regression

    ## [1] "The estimated mean squared test error for a ridge penalised linear regression model = 0.0174"

### Lasso Penalised Linear Regression

    ## [1] "The estimated mean squared test error for a lasso penalised linear regression model = 0.0176"

*Observations*

1.  The two penalised regression models perform about the same when
    using estimated mean squared test error as the metric of
    measurement.
