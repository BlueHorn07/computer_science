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
  - a.k.a. Covaroates, features, $p$-dim random vector, independent variables
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

- Two Supervised Learnings
  - **Regression**
    - Output $Y$ is <u>continuous</u>
    - Often, modeled as $Y = f(X) + \epsilon$
  - **Classification**
    - Output $Y$ is <u>categorical</u>
    - Often, we model $P(Y=k \mid X)$ (= 확률 추정)


