-   [Getting the Data](#getting-the-data)
-   [Introduction](#introduction)
-   [Ridge Penalised Linear Regression -
    Predictions](#ridge-penalised-linear-regression---predictions)
-   [Lasso Penalised Linear Regression
    Predictions](#lasso-penalised-linear-regression-predictions)
-   [Partial Least Squares
    Regression](#partial-least-squares-regression)
    -   [Scaling the data](#scaling-the-data)
    -   [Making Predictions](#making-predictions)
-   [Boosted Tree Ensemble](#boosted-tree-ensemble)
-   [Results](#results)

Loading the required libraries.

### Getting the Data

1.  We start by getting the previously cleaned *train* subset.

<!-- -->

    train = readRDS("../RDA/train")
    test = readRDS("../RDA/test")

### Introduction

1.  Comparing the multiple learning algorithms employed using the
    estimated mean squared test error as a measure of success, we
    shortlist the following to predict the `SalePrice` for the *test*
    dataset.
    1.  Ridge Penalised Linear Regression (est. test set error = 0.0174)
    2.  Lasso Penalised Linear Regression (est. test set error = 0.0176)
    3.  Partial Least Square Regression (estimated test set error =
        0.0587)
    4.  Boosted Tree Ensemble (estimated test set error = 0.015)
2.  We are including the Partial Least Square Regression Model to ensure
    that it performs as poorly on the test dataset as it does on the
    train set, thereby validating the approach taken through this entire
    project.

### Ridge Penalised Linear Regression - Predictions

1.  (From the help file) The results of `cv.glmnet` are random, since
    the folds are selected at random. We will therefore run `cv.glmnet`
    5 times, for each iteration compute the prediction for the test set
    and then average the prediction.

### Lasso Penalised Linear Regression Predictions

1.  We use the same strategy as for the Ridge Penalised model

### Partial Least Squares Regression

1.  The Partial Least Squares Regression requires scaling of the numeric
    features (ref. discussion earlier on the same topic)
2.  The results of `cross.val` are random, since the folds are selected
    at random. We will therefore run `cross.val` 5 times, for each
    iteration compute the prediction for the test set and then average
    the prediction. 3 We scale the *test* dataset features to the same
    scale as the respective feature in the *train* dataset

#### Scaling the data

#### Making Predictions

### Boosted Tree Ensemble

1.  We use the optimal interaction depth (= 4) and optimal learning rate
    (= 0.01) determined earlier through cross validation for the lowest
    estimated test error.

Results
-------

1.  We used four models to make predictions for the test dataset. The
    results, from the Kaggle evaluation, are as follows:

<table>
<thead>
<tr class="header">
<th align="left">Model</th>
<th align="center">Est Test Error</th>
<th align="center">Act Test Score</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Boosted Tree Ensemble</td>
<td align="center">0.0150</td>
<td align="center">0.12588</td>
</tr>
<tr class="even">
<td align="left">Ridge Penalised Regression</td>
<td align="center">0.0174</td>
<td align="center">0.12995</td>
</tr>
<tr class="odd">
<td align="left">Lasso Penalised Regression</td>
<td align="center">0.0176</td>
<td align="center">0.13111</td>
</tr>
<tr class="even">
<td align="left">Partial Least Square Regression</td>
<td align="center">0.0587</td>
<td align="center">0.41913</td>
</tr>
</tbody>
</table>

1.  It is quite satisfactory that the actual ranking of the models by
    test scores mirrors the ranking of the models by estimated test
    error validating the approach used in evaluating the different
    models
