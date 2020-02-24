# The *Ames Housing - Predict the Price* Challenge on www.kaggle.com

## Update 2020-02-24
The project is now implemented in Python too.

##  Introduction
The Ames Housing - Predict the Price presents an excellent case study for applying machine learning algorithm to derive insights, both causal and inferential.

In this project, I have focussed on applying multiple machine learning algorithm to the given data-set with a goal of reviewing their relative efficacy in predicting the prices of houses in the test dataset. I have applied 7 different algorithms - 2 parametric, 3 dimensionality reducing and 2 tree-based. The algorithms applied are:
1.  Ridge penalised Linear Regression
2.  Lasson penalised Linear Regression
3.  Principal Component Regression
4.  Partial Least Square Regression
5.  Best Subset Selection Regression
6.  Random Forest Trees Ensemble
7.  Boosted Trees Ensemble

The project is implemented in R.
    
##  The Challenge
The reasons that this makes an excellent case study especially for new practitioners on machine learning:
1.  **Domain knowledge** - To successfully address a machine learning problem, contextual familiarity is important. The ML practitioner must have reasonable knowledge of the domain from which the problem emerges. Since housing and housing prices are an integral part of everydat life, almost everyone has contextual familiarity and can easily build hypotheses to validate.
2.  **Moderate data size** - This challenge's data-set is moderate in size - both the number of examples as well as the *features* of the example. This helps the new practitoner as s/he is not burdened with additional data engineering challenges of managing resources to deal with large data-sets, allowing her/him to focus on implementing the machine learning algorithms.

The goal of the challenge is to learn from the *training* data-set and predict the survivors in the *test* data-set. The accuracy of the predictions is the measure of success.

##  My approach
The focus of my approach is to understand the relative efficacy of the different learning algorithms. Equally importantly, I was not focussed on *winning* the challenge but on using this as an opportunity to learn how a challenge may be addressed in a real-life situation.

The first two parts of my solution focusses on data wrangling and data analysis
1.  Performing exploratory data analysis on the train data-set to get better sense of the data and form preliminary hypotheses.
2.  Making changes to the data type of the features for both train and test data-sets to better reflect the *information* contained in them.
3.  Imputing missing values to features in both the train and test data-sets.
4.  Drawing *learning curves* to better inform the choice of the learning algorithms to use and the ranges of parameter values to test for in each of the chosen learning algorithm.

When applying the various learning algorithms I use the *train-validate-test* strategy to choose the optimal values of different parameters relevant to the specific learning algorithm and to estimate the likely test error.

The third part of my solution applies the penalised linear regression algorithm.

The fourth part of my solution applies other parametric learning alogrithms that focus on dimensionality reduction - Principal Components Regression, Partial Least Square Regression and Best Subset Selection.

The fifth part of my solution applies tress based learning algorithms - random forest ensemble and boosted trees ensemble.

For each of the learning algorithm I estimated the test set prediction accuracy and in the final, sixth, part I use the top 4 performing algorithms - ridge penalised linear regression, lasso penalised linear regression, partial least square regression and boosted trees ensemble -  to make predictions for the test data-set. We use Kaggle's evaluation engine to get final verified results of the performance of these 4 algorithms.

##  The Directory Structure
The entire project is available either as a single markdown document `Ames-Housing-Data.md` in the root directory or split into 6 sections, paralleling the discussion above, in the `/scripts` directory. The data, both input and output is in the `/data` directory. Finally the `/RDA` directory contains the RData created and used by the code in both the single document version and the 6-sections version.

### Update 2020-02-34
Added `/Python/scripts/` that hosts the Python code. Additionally the `Python/wip-data` directory contains intermediate data files.
