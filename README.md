## Credit risk default prediction: Project overview
This is a repository for [Home Credit Default Risk](https://www.kaggle.com/c/home-credit-default-risk) competition that was hosted on Kaggle. The objective of this competition was to use data from various sources like credit bureau, previous loan applications, previous loan performance, previous credit card performance, installment payments and current application data in order to predict the probability of default of the applicant. The output of this model (in form of scores or risk bands) can then be used to make a credit decision (approve/reject) regarding the application.

## Approach
**Part 1 :** We import all the datasets and do a basic exploratory analysis to understand the data provided to us. The data from various sources like previous loan applications, installment payments, previous loan performance etc. needs to be mapped on the training data (current application details). In order to do this we have to create aggregated variables on current applciation id (SK_ID_CURR) and then map it on training data. The notebook **1. Aggregate variables and mapping on train data.ipynb** contains the code to accomplish this.

**Part 2 :** In the second part we do a detailed EDA post mapping the aggregated data on the training set. However, given the high number of features (213 numeric + categorical) we opt for a strategy of filtering certain unimportant features basis bivariate analysis using Weight of evidence (WOE) and Information value (IV) before doing EDA. We eliminate features with IV < 0.02 and then handle missing values and other quirks in the shortlisted features. We build a baseline logistic regression model using all these features to get a baseline ROC score. We then further improve this score by doing some more feature engineering & eliminating unimportant variables using RFECV (recursive feature elimination with cross validation). Refer **2. EDA & Baseline model with Logistic regression.ipynb** for this part.

## Results & outcome
| Model version | ROC score | Kaggle performance (on test data) |
| ------------- | ----------- | ----------------- |
| Logistic regression (baseline) | 0.6303 | 0.6109 |
| Logistic regression (After feature selection) | 0.7486 | 0.7351 |

## Next steps & future work
1. Currently bureau data given as part of the competition has not been used in the model. We expect significant improvement in model performance post using bureau features.
2. We can check if we can improve the current best model by trying some hyperparameter tuning and removing certain correlated features.
3. Try ensembling algorithms like Random forests and Gradient boosting (LightGBM implementation as it handles missing data) to see if it improves model performance any further.
