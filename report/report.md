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

## 3. Methods

Our analysis contains five different learning algorithms, that includes `Kernel Ridge Regression`(KRR), `Lasso Regression`, `ElasticNet`, `Decision Tree` and `Multi-layer Perceptron Regressor`(MLPRegressor). We are explaining each of the algorithms subsequently:

### 3.1 ElasticNet

原理，基于L1与L2进行正则化。公式：
$$
L(\bar{w})=\frac{1}{2 n}\|X \bar{w}-\bar{y}\|_{2}^{2}+\alpha \beta\|\bar{w}\|_{1}+\frac{\alpha(1-\beta)}{2}\|\bar{w}\|_{2}^{2}
$$


reference link:

- [变量的选择——Lasso&Ridge&ElasticNet - 冬色 - 博客园 (cnblogs.com)](https://www.cnblogs.com/mengnan/p/9307615.html)
- [机器学习算法之岭回归、Lasso回归和ElasticNet回归 – 标点符 (biaodianfu.com)](https://www.biaodianfu.com/ridge-lasso-elasticnet.html)



这篇解释蛮不错的，在写这部分的原理之前，可以参考一下。

### 3.2 Decision Tree

### 3.3 Multi-layer Perceptron Regressor

## 4. Experiments/Results/Discussion

### 4.1 ElasticNet

### 4.2 Decision Tree

### 4.3 Multi-layer Perceptron Regressor

## 5. Summary

## 6. Contributions

## 7. Appendix

