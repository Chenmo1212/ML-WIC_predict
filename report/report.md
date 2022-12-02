# Project Report: WIC Prediction

---

Group: 18

Member:

- YILUN LI
- LONG PAN
- QIGUANG WANG

---

## 1. Introduction

`WIC` is an American federal assistance program for health-care and nutrition, which aims to safeguard the health of low-income women, infants, and children up to age 5 who are at nutrition risk by providing nutritious foods to supplement diets, information on healthy eating, and referrals to health care. `WIC` made a difference for over 196,000 women, infants and children in Washington in 2021.

 The data about the Food Environment Atlas  are released by U.S. DEPARTMENT OF AGRICULTURE in the official DEPARTMENT OF AGRICULTURE website. The Atlas assembles statistics on three broad categories of food environment factors: **Food Choices**, **Health and Well-Being** and **Community Characteristics**. The Atlas currently includes more than 280 indicators of the food environment. The year and geographic level of the indicators vary to better accommodate data from a variety of sources. Some indicators are at the county level while others are at the State or regional level. The most recent county-level data are used whenever possible.

Based on the data and the number of participants in `WIC` over the years, we are trying to build some models to predict the number of participants in `WIC` in the future.

## 2. Dataset and Features

This file consists of 31481 lines of data and contains smultiple spreadsheets:
 - A variable list that includes metadata about all of the variables that are mapped in the Food Environment Atlas.
 - Spreadsheets that contain data for each of the Food Environment Atlas categories.
 - County- and State-level supplemental data that were used as the basis for a number of calculations in the Food Environment Atlas.

We acquire our data of the Food Environment Atlas from the open data website of U.S. Department of Agriculture. After basic detection of the dataset, we decided to delete the duplication lines in all spreadsheets. Considering that there are obvious correlations between some of the initially chosen features, such as the poverty rate of a city and the child poverty rate, we need to perform a correlation analysis for each group of variables that may be correlated, and then pick up some features that can be used for training the model. Here, the Pearson correlation coefficients between different features in each group are calculated to determine their linear correlations, thus achieving a preliminary correlation analysis as a part of feature seletion.
During data import phase, we normalize data by convert feature values from their original range into a standard range (0,1) while calculating the means and standard deviations of cross_val_score. To visualize its scores, we plot error bar to display the graph.
The initial set of faetures set is: 
|               |                |                 |                 |                   |                 |   |   |   |   |
|:-------------:|:--------------:|:---------------:|:---------------:|:-----------------:|:---------------:|:---:|:---:|:---:|:---:|
| LACCESS_POP15 | LACCESS_LOWI15 | LACCESS_HHNV15  | LACCESS_CHILD15 | LACCESS_SENIORS15 | POVRATE15       |   |   |   |   |
| GROCPTH16     | SUPERCPTH16    | CONVSPTH16      | SPECSPTH16      | WICSPTH16         | CHILDPOVRATE15  |   |   |   |   |
| FFRPTH16      | FSRPTH16       | FOODINSEC_15_17 | VLFOODSEC_15_17 | FMRKT_WIC18       | FMRKT_WICCASH18 |   |   |   |   |

And the seleted features set is:

|             |                 |                          |               |           |   |   |   |   |   |
|:-----------:|:---------------:|:------------------------:|:-------------:|:---------:|:---:|:---:|:---:|:---:|:---:|
| County      | State           | Population_Estimate_2016 | LACCESS_POP15 | GROCPTH16 |   |   |   |   |   |
| SUPERCPTH16 | CONVSPTH16      | SPECSPTH16               | WICSPTH16     | FFRPTH16  |   |   |   |   |   |
| FSRPTH16    | FOODINSEC_15_17 | FMRKT_WIC18              | POVRATE15     | PCT_WIC17 |   |   |   |   |   |



## 3. Methods

Our analysis contains five different learning algorithms, that includes `Kernel Ridge Regression`(KRR), `Lasso Regression`, `ElasticNet`, `Decision Tree` and `Multi-layer Perceptron Regressor`(MLPRegressor). We are explaining each of the algorithms subsequently:

### 3.1 ElasticNet

Elastic net linear regression uses a weighted penalties combined from both the lasso and ridge regression models to overcome the limitations of the LASSO. Below is the cost function for ElasticNet.
\displaystyle\min\limits_{w}\frac{1}{2n_{samples}}\lVert X_{w}-Y\rVert_2^2+\alpha\rho\lVert W\rVert_1+\frac{\alpha\lgroup 1-\rho\rgroup}{2}\ \lVert W\rVert_2^2

### 3.2 Decision Tree

Decision Trees (DTs) are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. A deision tree can be seen as a piecewise constant approximation. Here, we apply DecisionTreeRegressor of which the decision or the outcome variable is Continuous to our regression problem. The randomness of DecisionTreeRegressor is decided by using random_state as a seed for random selection of features. So we finalize it via cross validation estimator and set random_state to 913.

### 3.3 Multi-layer Perceptron Regressor

A neural network is a combination of lots of general process units. MLP is a type of artificial neural network (ANN). Its simplest form consists of at least three layers of nodes: an input layer, a hidden layer and an output layer. MLP is a feed-forward neural network where all neurons are arranged in an acyclic graph. We still evalute the l1_ratio of MLP by cross-validation 

## 4. Experiments/Results/Discussion

### 4.1 ElasticNet

### 4.2 Decision Tree

### 4.3 Multi-layer Perceptron Regressor

## 5. Summary

## 6. Contributions

## 7. Appendix

