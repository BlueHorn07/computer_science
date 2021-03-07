---
title: "Overview of Supervised Learning"
layout: post
use_math: true
tags: ["Statistical Data Mining"]
---

### 서론
2021-1학기, 대학에서 '통계적 데이터마이닝' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<br><span class="statement-title">TOC.</span><br>

- Set-up


<hr/>

### Set-up

- **Input Variables**: $X = (X_1, \dots, X_p)^T$
  - a.k.a. Covariates, features, $p$-dim random vector, independent variables
- **Output Variables**: $Y$
  - a.k.a. Responses, $y$-values random variable, dependent variables
- **Data**: $\\{(y_1, x_1), \dots, (y_n, x_n)\\}$
  - Realization of $(X, Y)$ (often regarded as i.i.d. <small>*independent and identically distributed*</small>)

### Variable types

- **Qauntitive Variables**
  - Continuous variables
- **Qualitive Variables**
  - Discrete variables or Categorical Variables
- **Ordinal Variables**
  - ex: small < medium < large

<hr/>

- Two Supervised Learnings Tasks
  - **Regression**
    - Output $Y$ is <u>continuous</u>
    - Often, modeled as $Y = f(X) + \epsilon$
    - **Goal**: construct good model $f$ with low $\epsilon$
  - **Classification**
    - Output $Y$ is <u>categorical</u>
    - Often, we model $P(Y=k \mid X)$ (= 확률 추정)
    - **Goal**: construct good model to determine output value with given $X$.s

<hr/>

\<Supervised Learning\>에선 문제를 해결하기 위해, 아래의 두 가지 접근을 취한다.

- Least Squared Estimator
- Nearest Neighbor

이 두 접근법은 \<Supervised Learning\> 문제를 해결하는 가장 기본이 된다.


<br><span class="statement-title">Definition.</span> Linear Model<br>

Given input $X = (X_1, \dots, X_p)^T$, we predict $Y$ as

$$
\hat{Y} = \hat{\beta_0} + \sum^{p}_{i=1} {\hat{\beta_i} X_i}
$$

- 일반적으로 hat($\hat{x}$)이 있으면, predicted value로 취급한다.
- $\beta_i$는 'regression coefficient'라고 한다. 특히, $\beta_0$를 \<intercept\> 또는 \<bias\>라고 한다.
  - 편의를 위해 $X_0=1$라고 설정할 수도 있다.
  - 이 경우, 식은 $\hat{Y} = X^T \hat{\beta}$가 된다.

### Least Squared Estimator

그럴듯한 $\hat{\beta}$를 추정하기 위해 "residual sum of squares"를 최소화하는 **LSE**의 접근을 취할 수 있다.

$$
\begin{aligned}
  \mbox{RSS}(\beta) &= \sum^n_{i=1} (y_i - {x_i}^T \beta)^2 \\
  &= (\mathbf{y} - \mathbf{X}\beta)^T(\mathbf{y} - \mathbf{X}\beta)
\end{aligned}
$$

위 식에서 $\mathbf{y}$, $\mathbf{X}$는 각각 아래의 의미를 가진다.

- $\mathbf{y}$는 정답 레이블을 모은 vector로 \<response vector\>라고 한다.

$$
\mathbf{y} = \left( y_1, \dots, y_n \right)^T
$$

- $\mathbf{X}$는 입력되는 feature vector를 모은 matrix로 \<design matrix\>라고 한다.

$$
\mathbf{X} = \left( x_1, \dots, x_n \right)^T
$$

\<design matrix\>를 다르게 표현하면 아래와 같다.

$$
\mathbf{X} = \left( x_1, \dots, x_n \right)^T = \left( \mathbf{x}_1, \dots, \mathbf{x}_p \right)
$$

첫번째 표기는 $p$-dim feature vector $n$개를 차곡차곡 표현한 것이고, 두번째 표기는 $n$개 feature vector에서 feature $x_i$ 하나에 대한 값을 모두 모아 vector $\mathbf{x}_i$로 표현했다.

<br/>

LS 접근에서는 $\hat{\beta}$를 아래와 같이 추정한다.

$$
\begin{aligned}
\hat{\beta} &= \underset{\beta \in \mathbb{R}^p}{\text{argmin}} \; \mbox{RSS}(\beta) \\
&= \left( \mathbf{X}^T \mathbf{X}\right)^{-1} \mathbf{X}^T \cdot \mathbf{y}
\end{aligned}
$$

