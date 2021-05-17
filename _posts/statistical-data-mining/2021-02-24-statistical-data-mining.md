---
title: "Statistical Data Mining"
layout: post
use_math: true
tags: ["Statistical Data Mining"]
hidden: true
---

<br/>

2021-1학기에 수강한 채민우 교수님의 "**통계적 데이터 마이닝(IMEN472)**" 수업에서 배운 것과 공부한 것을 정리한 지킬 블로그입니다. 개인적으로 본인이 처음 도전해보는 분야고 응용 수학의 수많은 테크닉들을 사용하기 때문에 수업을 따라가는게 쉽지는 않았습니다만, 본 수업을 통해서 데이터 사이언스에 대한 프론티어를 맛볼 수 있었습니다. 🤯

#### 참고 교재
- [『The Elements of Statistical Learning』](https://web.stanford.edu/~hastie/ElemStatLearn/) Trevor Hastie · Robert Tibshirani · Jerome Friedman, 2nd ed.
- [『An Introduction to Statistical Learning』](https://www.statlearning.com/) Gareth James · Daniela Witten · Trevor Hastie · Robert Tibshirani, 1st ed.
- [CS229: Machine Learning](http://cs229.stanford.edu/syllabus-autumn2018.html), Andrew Ng, Stanford Univ. [^1]

<div class="math-statement" markdown="1" style="padding: 10px 20px">

[목차]

1. Supplemnetary
2. Introduction
3. Linear Regression
4. Linear Classification
5. Non-parametric Method
6. Decision Tree
7. Boosting 🔥
8. Random Forest 🔥
9. SVM; Support Vector Machine
10. PCA; Principle Component Analysis 🔥
11. Clustering

</div>

<hr/>

### Supplementary

앞으로 이어지는 "통데마"의 실전을 마주하기 전에 "**반드시**" 알아야 하는 내용들입니다. 모든 내용과 수학적 표현과 추상화에 충분히 익숙해져야 합니다.

<details markdown="1" class="statement">
<summary>펼쳐보기</summary>

#### Linear Algebra

- [Basic Linear Algebra]({{"/2021/03/07/supp-1-linear-algebra-1.html" | relative_url}})
  - Column space & Row space & Null space
  - Fundamental Theorem of Linear Algebra
  - Eigen value & Eigen vector 

- [Vector Calculus & Matrix Calculus]({{"/2021/03/08/supp-1-linear-algebra-2.html#matrix-calculus" | relative_url}})
- [Spectral Decomposition & Singular Value Decomposition]({{"/2021/03/14/supp-1-linear-algebra-3.html" | relative_url}})

#### Multivariate Normal Distribution

#### Conditional Expectation

</details>

<hr/>

### [Introduction]({{"/2021/02/26/overview-of-supervised-learning.html" | relative_url}})

- Introduction to Regression & Classification
  - Least Squared Method
  - Nearest Neighbor Method
- Curse of dimentionality

<hr/>

### Linear Methods for Regression

- [Feature Selection]({{"/2021/05/16/feature-selection-techniques.html" | relative_url}})
  - Best Subset Selection
  - Forward Stepwise Selection
  - Backward Stepwise Selection
  - Mallow's $C_p$
  - AIC & BIC
  - Instability of Variable Selection

- Shrinkage Method

- Lasso Regression
- Ridge Regression

<hr/>

### Non-parametric Method

- [Non-parametric Linear Regression]({{"/2021/04/18/regression-spline.html" | relative_url}})
  - Polynomial Regression
    - Local Polynomical Regression
  - [Regression Spline]({{"/2021/04/18/regression-spline.html#regression-spine" | relative_url}}) 🔥
  - Natural Cubic Spline
    - power basis function
  - Smoothing Splines
    - knot selection
  - [Non-parametric Logistic Regression]({{"/2021/04/19/splines-method-2.html#non-parameteric-logistic-regression" | relative_url}})
  - [Multi-dimensional Splines]({{"/2021/04/19/splines-method-2.html#multi-dimensional-splines" | relative_url}})

- [KNN Method]({{"/2021/05/16/KNN-and-kernel-method.html" | relative_url}})
  - [kernel method]({{"/2021/05/16/KNN-and-kernel-method.html#kernel-method" | relative_url}})
- Nadaraya-Watson Estimator

- Additive Model
- Backfitting Algorithm
- Generalized Additive Models 🔥
- MARS; Multivariate Adaptive Regression Spline 🔥


<hr/>

### Boosting

- AdaBoost
- Gradient Boosting
- XGBoost

### Random Forest



<hr/>

[^1]: 수업의 일부 토픽에서 CS229에서 배운 부분이 종종 등장했습니다. CS229에서 통계적 접근을 통해 고전적인 머신 러닝을 다루기 때문에 두 과목을 공부하는 데에 양방향으로 도움을 많이 받았습니다 😊


