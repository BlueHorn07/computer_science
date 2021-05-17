---
title: "KNN & kernel method"
layout: post
use_math: true
tags: ["Statistical Data Mining"]
---

### 서론
2021-1학기, 대학에서 '통계적 데이터마이닝' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

이 포스트는 [Regression Spline]({{"/2021/04/18/regression-spline.html" | relative_url}})과 [Spline Method (2)]({{"/2021/04/19/splines-method-2.html" | relative_url}})이어지는 내용입니다 😊

<br><span class="statement-title">TOC.</span><br>

- KNN; K-Nearest Neighbor method
- kernel method
- Nada

<hr/>

### KNN; K-Nearest Neighbor method

Regression function $f(x) = E(Y \mid X=x)$를 모델링 하는 가장 자연스러운 접근중 하나는 바로 $x$에 가장 가까운 $k$개의 점으로 평균을 내는 \<KNN\>이다.

$$
\hat{f}(x) = \text{Avg} \, (y_i \, \mid \, x_i \in N_k(x))
$$

where $N_k(x)$ is the set of $k$ points nearest to $x$.

이렇게 KNN을 쓸때 깔린 가정은 <span class="half_HL">"추정하려는 함수 $f(x)$가 smooth 하다"</span>이다.

KNN의 parameter인 $k$는 model complexity를 컨트롤 한다.

- small $k$: model complexity ▲, bias ▼, variance ▲ <small>// make ziggle model</small>
- Large $k$: model complexity ▼, bias ▲, variance ▼ <small>// make smooth model</small>

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/knn-1.png" | relative_url }}" width="500px">
</div>

[Problem 😱] KNN $\hat{f}(x)$ is <span style="color:red">**not smooth**</span> and <span style="color:red">**not continuous**</span>!!

<br/>

KNN의 문제를 해결하기 위해 도입하는 것이 바로 \<kernel method\>다!

<hr/>

### Kernel Method

KNN의 식을 다시 기술해보면 아래와 같다.

$$
\hat{f}(x) = \frac{\displaystyle \sum^n_{i=1} \, K_k (x, x_i) \cdot y_i}{\displaystyle \sum^n_{i=1} \, K_k (x, x_i) }
$$

where $K_k (x, x_i) = I(x_i \in N_k (x))$.

\<kernel method\>의 메인 아이디어는 <span class="half_HL">KNN에서 $I(x_i \in N_k(x))$를 다른 smooth function $K_{\lambda}(x, x')$로 대체한다</span>는 것이다!! 이때의 그 smooth function $K_{\lambda}(x, x')$를 \<**kernel function**\>이라고 한다!!

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/kernel-method-1.png" | relative_url }}" width="550px">
</div>

위의 그림은 \<kernel function\> 중 하나인 \<Epanechnikov kernel\>을 시각화한 것이다.


