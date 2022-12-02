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

We acquire our data of the Food Environment Atlas from the open data website of U.S. Department of Agriculture. After basic detection of the dataset, we decided to delete the duplication lines in all spreadsheets. Considering that there are obvious correlations between some of the initially chosen features, such as the poverty rate of a city and the child poverty rate, we need to perform a correlation analysis for each group of variables that may be correlated, and then pick up some features that can be used for training the model. Here, the `Pearson` correlation coefficients between different features in each group are calculated to determine their linear correlations, thus achieving a preliminary correlation analysis as a part of feature selection.

During data import phase, we normalize data by convert feature values from their original range into a standard range (0,1), while calculating the means and standard deviations of `cross_val_score`. To visualize its scores, we plot `heatmap` to display the result.

The initial feature groups are: 

- LACCESS_POP15, LACCESS_LOWI15, LACCESS_HHNV15, LACCESS_CHILD15, LACCESS_SENIORS15
- GROCPTH16, SUPERCPTH16, CONVSPTH16, SPECSPTH16, WICSPTH16
- FFRPTH16, FSRPTH16
- FOODINSEC_15_17, VLFOODSEC_15_17
- FMRKT_WIC18, FMRKT_WICCASH18
- POVRATE15, CHILDPOVRATE15

Here is the heatmap of correlation:

> ![total](report.assets/total.jpg)
>
> <p align=center>Figure 1: Heat map plot of different feature groups</p>

Through the correlation results, it can be seen that there is a great correlation in the first group, so after discussion, we choose to leave `LACCESS_POP15` as a feature. There is a low correlation in the second group, so we can leave all features. In the end, we left a total of 12 variables. Use the following code to use the filtered variables as data for machine learning：

```python
preserve_columns = ['State','LACCESS_POP15','GROCPTH16', 'SUPERCPTH16', 'CONVSPTH16', 'SPECSPTH16', 'WICSPTH16', 'FFRPTH16', 'FSRPTH16', 'FOODINSEC_15_17', 'FMRKT_WIC18', 'POVRATE15', 'PCT_WIC17']

raw_data['PCT_WIC17'] = raw_data['PCT_WIC17'] * raw_data['Population_Estimate_2016'] / 100
raw_data['FOODINSEC_15_17'] = raw_data['FOODINSEC_15_17'] * raw_data['Population_Estimate_2016'] / 100
raw_data['POVRATE15'] = raw_data['POVRATE15'] * raw_data['Population_Estimate_2016'] / 100

raw_data = raw_data[preserve_columns]
```


## 3. Methods

Our analysis contains three different learning algorithms, that includes `ElasticNet`, `Decision Tree` and `Multi-layer Perceptron Regressor`(MLPRegressor). We are explaining each of the algorithms subsequently:

### 3.1 ElasticNet

We have learned `Ridge` regression and `Lasso `regression are two regression methods. They appear to solve the over-fitting of linear regression and the irreversibility of $(X^TX)$ in the process of solving $θ$ through the normal equation method. For the class of problems, both regressions achieve their goals by introducing a regularization term in the loss function. In order to prevent over-fitting ( $θ$ is too large), a complexity penalty factor, that is, a regular term, is added after the objective function $J(\theta)$ to prevent over-fitting.

The loss function of `ElasticNet` is:
$$
L(\bar{w})=\frac{1}{2 n}\|X \bar{w}-\bar{y}\|_{2}^{2}+\alpha \beta\|\bar{w}\|_{1}+\frac{\alpha(1-\beta)}{2}\|\bar{w}\|_{2}^{2}
$$
As can be seen from the above formula, two parameters $α$ and $β$ need to be provided when using `ElasticNet`. The name of the parameter in $β$ is **L1_ratio**. In the experimental part, these two parameters will be tuned using cross-validation.

### 3.2 Decision Tree

`Decision Trees` (DTs) are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. A `decision tree` can be seen as a piecewise constant approximation. Here, we apply `DecisionTreeRegressor` of which the decision or the outcome variable is Continuous to our regression problem. The randomness of `DecisionTreeRegressor` is decided by using random_state as a seed for random selection of features. So we finalize it via cross validation estimator and set random_state to 23. In addition, we will use cross-validation to train the **max_depth** parameter of the decision tree in the experimental part.

### 3.3 Multi-layer Perceptron Regressor

A neural network is a combination of lots of general process units. `MLP` is a type of artificial neural network (ANN). Its simplest form consists of at least three layers of nodes: an input layer, a hidden layer and an output layer. `MLP` is a feed-forward neural network where all neurons are arranged in an acyclic graph. We still evaluate the `l1_ratio` of `MLP` by cross-validation. In addition, we will use cross-validation to train the **hidden_layer_sizes** parameter and **learning_rate_init** of the decision tree in the experimental part.

## 4. Experiments/Results/Discussion

### 4.1 ElasticNet

### 4.2 Decision Tree

### 4.3 Multi-layer Perceptron Regressor

## 5. Summary

## 6. Contributions

## 7. Appendix

