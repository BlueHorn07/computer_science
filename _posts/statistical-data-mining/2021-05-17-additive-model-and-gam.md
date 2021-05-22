---
title: "Additive Model & GAM"
layout: post
use_math: true
tags: ["Statistical Data Mining"]
---

### 서론
2021-1학기, 대학에서 '통계적 데이터마이닝' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<br><span class="statement-title">TOC.</span><br>

- Additive Model
  - Backfitting Algorithm
- GAM; Generalized Additive Model

<hr/>

The regression model 

$$
E (Y \mid X_1, \dots, X_p) = \alpha + f_1(X_1) + \cdots + f_p(X_p)
$$

is called an \<additive model\>.

<span class="half_HL">It assumes that there is no interaction effect.</span>

Therefore, it can effectively avoid "the curve of dimensionality".

✨ Goal: How can we estimate $f_i(x_i)$?

이때 쓰는 접근법이 바로 \<Backfitting Algorithm\>이다.

<br/>

보통 우리가 $f_j$를 제외한 나머지 $f_k$에 대한 함수를 알고 있을 때, $f_j$를 추정하는 것은 아주 쉽다. 그냥 1차원 문제를 해결하는 것이기 때문이다!

이렇게 다른 함수를 fix 시켜두고, 함수 하나를 fitting 하는 기법을 \<Backfitting Algorithm\>이라고 한다.'

<div class="math-statement" markdown="1">

<span class="statement-title">Algorithm.</span> Backfitting Algorithm<br>

1\. Initialize: <br/>
\- $\hat{\alpha} = \bar{y}$<br/>
\- for $\forall \, j$, $\hat{f}_j = 0$

2\. Repeat until converge

find an estiamtor $\hat{f}_j$ based on $$\left\{ x_i, \; y_i - \hat{\alpha} - \displaystyle \sum_{k\ne j} \hat{f}_k(x_{ik}) \right\}^n_{i=1}$$

</div>

💥 이때, 2번째 스텝에서 \<smoothing spline\>이나 \<kernel method\> 등의 다른 non-parameteric method들을 적용해볼 수도 있다.

\<Backfitting Algorithm\>은 Convex optimization과 비슷하다고 하며, 굉장히 빠르게 수렴한다고 한다! 😲

<hr/>

### GAM; Generalized Additive Model

\<GAM; Generalized Additive Model\>은 강력하면서도 간단한 통계적 테크닉 중 하나이다. 1986년, ESL의 공동저자인 "Trevor Hastie"와 "Robert Tibshirani"에 의해 개발된 방법이다.

<div class="statement" markdown="1">

Relationships btw the individual predictors and the dependent variable follow <u>smooth patterns</u> that can be linear or non-linear.

</div>

즉, GAM은 \<Additive Model\>에서 $f_j$가 <u>smooth non-parametric</u>인 경우를 다루는 모델이다!

'multithreaded'에 게시된 [포스트](https://multithreaded.stitchfix.com/blog/2015/07/30/gam/)에서는 GAM의 장점으로 

(1) Interpretability<br/>
(2) Flexibility & Automation<br/>
(3) Regularization

을 꼽는다.

이 중에서 먼저 "Regularization"부터 살펴보자. smooth function을 추정하는 **GAM**은 "smoothness"를 컨트롤 하는 tuning parameter $\lambda$가 존재한다. 이것을 통해 overfitting을 방지하고, 전체 predictor가 wiggle 해지는 것을 방지한다.



#### 참고자료

- [post from 'multithreaded'](https://multithreaded.stitchfix.com/blog/2015/07/30/gam/)