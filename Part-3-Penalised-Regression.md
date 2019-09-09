-   [Getting the Data](#getting-the-data)
-   [Introduction](#introduction)
-   [Unpenalised Linear Regression](#unpenalised-linear-regression)
-   [Ridge Penalised Linear
    Regression](#ridge-penalised-linear-regression)
-   [Lasso Penalised Linear
    Regression](#lasso-penalised-linear-regression)

Loading the required libraries.

Loading required functions.

    na.count = function (dat){
      dat %>% apply(., 2, is.na) %>% apply(.,2,sum) %>% .[.!=0]
    }

### Getting the Data

1.  We start by getting the previously cleaned *train* subset.

<!-- -->

    train = readRDS("./RDA/train")

### Introduction

1.  We will build both the ridge penalised and lasso penalised
    regression models.
2.  We will use the *train-validate-test* strategy to fit an optimal
    model to the *train* data-set as well as estimate the likely test
    error.
3.  The train data-set will be divided into 2 subsets - **train** and
    **test** - in the ratio 70:30.
4.  The *train* subset will be used to build the model. The `glmnet`
    library has an inbuilt cross-validation feature that allows for
    selection of optimal penalty factor *lambda*.
5.  The *test subset* will be used to estimate the likely test error.
6.  We first establish a baseline by estimating the likely test error
    for an un-penalised linear regresssion model.

### Unpenalised Linear Regression

    n = nrow(train)
    x = model.matrix(SalePrice~., data = train)[,-1]
    y = train$SalePrice %>% log()
    est.test.err = 0
    for (k in 1:5) {
        set.seed(k)
        indx = sample(1:n, 0.7*n)
        
        fit = glmnet(x[indx,], y[indx], family = "gaussian", alpha = 0, lambda = c(10^-10, 0))
        bestlambda = cv.glmnet(x[indx,], y[indx], alpha = 0, lambda = c(10^-10, 0), type.measure = "mse")$lambda.min
        
        y.test.hat = predict(fit, newx = x[-indx,], s = bestlambda, type = "response") %>% as.numeric()
        test.error = (y.test.hat-y[-indx])^2 %>% mean() %>% sqrt()
        est.test.err = est.test.err + test.error
    }

    est.test.err = round(est.test.err/5, digits = 4)

    print(paste("The estimated test error for a un penalised linear regression model =", est.test.err))

    ## [1] "The estimated test error for a un penalised linear regression model = 0.1467"

### Ridge Penalised Linear Regression

    est.test.err = 0
    for (k in 1:5) {
        set.seed(k)
        indx = sample(1:n, 0.7*n)
        
        fit = glmnet(x[indx,], y[indx], family = "gaussian", alpha = 0)
        bestlambda = cv.glmnet(x[indx,], y[indx], type.measure = "mse")$lambda.min
        
        y.test.hat = predict(fit, newx = x[-indx,], s = bestlambda, type = "response") %>% as.numeric()
        test.error = (y.test.hat-y[-indx])^2 %>% mean() %>% sqrt()
        est.test.err = est.test.err + test.error
    }

    est.test.err = round(est.test.err/5, digits = 4)

    print(paste("The estimated test error for a ridge penalised linear regression model =", est.test.err))

    ## [1] "The estimated test error for a ridge penalised linear regression model = 0.1324"

### Lasso Penalised Linear Regression

    est.test.err = 0
    for (k in 1:5) {
        set.seed(k)
        indx = sample(1:n, 0.7*n)
        
        fit = glmnet(x[indx,], y[indx], family = "gaussian", alpha = 1)
        bestlambda = cv.glmnet(x[indx,], y[indx], type.measure = "mse")$lambda.min
        
        y.test.hat = predict(fit, newx = x[-indx,], s = bestlambda, type = "response") %>% as.numeric()
        test.error = (y.test.hat-y[-indx])^2 %>% mean() %>% sqrt()
        est.test.err = est.test.err + test.error
    }

    est.test.err = round(est.test.err/5, digits = 4)

    print(paste("The estimated test error for a lasso penalised linear regression model =", est.test.err))

    ## [1] "The estimated test error for a lasso penalised linear regression model = 0.1302"

*Observations*

1.  Of the two penalised regression models, the lasso regression model
    performs better on the estimated test error metric.
