---
title: "Regression Spline"
layout: post
use_math: true
tags: ["Statistical Data Mining"]
---

### 서론
2021-1학기, 대학에서 '통계적 데이터마이닝' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<br><span class="statement-title">TOC.</span><br>

- Basis Expansion
- Polynomial Regression
- Regression Spline
  - spline basis function
- Natural Cubic Spline

<hr/>

이전 챕터에서는 parameter를 추론해 linear regreeion & linear classification을 수행하는 방법을 살펴보았다.

$$
f(x) = E[Y \mid X = x] = \beta^T x
$$

이번 챕터에서는 **non-linear model**에 대해 살펴볼 예정이며, \<Basis Expansion\>과 \<Kernel Method\>을 중심으로 non-linear model을 살펴본다!

<hr/>

### Basis Expansion

<span class="statement-title">Definition.</span> Basis expansion<br>

For $m=1, \dots, M$, let $h_m: \mathbb{R}^p \rightarrow \mathbb{R}$ be the $m$-th **transformation** of $X$.

Then, we model as 

$$
f(X) = \sum^M_{m=1} \beta_m h_m (X)
$$

with a **<u>linear basis expansion</u>** in $X$.

<br/>

<span class="statement-title">Example.</span><br>

1\. feature dim $p$로 분할

$$
h_m(X) = X_m \quad \text{for} \quad m=1, \dots, p
$$

2\. Covariatic Transform <small>(정식 명칭은 아니고, Cov 같은 느낌이라 본인은 이렇게 부른다.)</small>

$$
h_m (X) = X^2_j \quad \text{or} \quad h_m(X) = X_j X_k
$$

3\. log transform or root transform

$$
h_m(X) = \log (X_j) \quad \text{of} \quad h_m (X) = \sqrt{X_j}
$$

4\. range transform

$$
h_m(X) = I(L_m \le X_k < U_m)
$$

특정 범위에 따라 $X_k$를 제단하는 transform이다.

<br/>

5\. **Splines** 🔥

곧 만날 예정!

<br/>

6\. Wavelet bases

정말 중요하게 쓰이는 방법이지만, 정규 수업에서는 다루지 않았다.

<hr/>

### Polynomial Regression

<div class="statement">

"Every smooth function can be approximated by polynomials!" <br/>

<small style="color: grey">-- Weierstrass's Approximation Theorem</small>

</div>

For $p$-dimensional $X$, the $m$-th order polynomial is given as

$$
f(X) = \beta_0 + \left(\sum^p_{j=1} \beta_j X_j\right) + \left(\sum^{p^2}_{j,k} \beta_{jk} X_j X_k\right) + \cdots + \left(\sum^{p^m}_{j_1, \dots, j_m} \beta_{j_1, \dots, j_m} X_{j_1} \cdots X_{jm} \right)
$$

- As $p$ increases, the # of parameters grows exponentially.
- In general, it is difficult to estimate $p$-dimentional regression function for large $p$.

논의 편의를 위해 $p=1$라고 하자. 그리고, $X_i$를 아래와 같이 디자인 하자.

Let $X_1 \sim \text{Unif}(0, 1)$, and $X_m = X_1^m$ for $m \le 4$.

이때, $X_1, \dots, X_4$의 Corr를 구해보면,

$$
\text{Corr}(X_1, \dots, X_4) = \begin{bmatrix}
    1.00 & 0.97 & 0.92 & 0.86 \\
    0.97 & 1.00 & 0.98 & 0.95 \\
    0.92 & 0.98 & 1.00 & 0.99 \\
    0.86 & 0.95 & 0.99 & 1.00
\end{bmatrix}
$$

와 같은데, Corr의 값을 살펴보면, 모두 1에 가까운 값을 가진다. 이것은 각 <span class="half_HL">독립변수 사이에 강한 상관관계가 있다</span>는 것을 의미하며, 이것을 \<**Multi-collinearity**; 다중공선성\>이라고 한다.

- High order polynomials are often **unstable** at the boundary.

→ bad!!! 😥

<hr/>

### Local Polynomial Regression

<div class="statement">

"Every smooth function can be locally approximated by low dimentional polynomials!" <br/>

<small style="color: grey">-- Talyor's Theorem</small>

</div>

Supp. that $p=1$. Divide domain interval $(a, b)$ into $K+1$ sub-intervals $(a=\xi_0, \xi_1], (\xi_1, \xi_2], \dots, (\xi_k , b=\xi_{k+1})$.

Then, a local polynomial regression model is given as

$$
f(X) = \sum^{K+1}_{i=1} f_{i}(X) \cdot I(\xi_{i-1} < X \le \xi_i)
$$

where $f_i$ are polynomials and $\xi_i$ are the **<u>knots</u>**.

앞에서 살펴본 \<Polynomial Regression\>과 비교했을 때, <span class="half_HL">범위 전체를 도메인으로 갖는 polynomial을 취하는 것이 아니라 domain inteveral을 divide하여 polynomial을 취한다</span>는 점이 다르다.

<br/>

<span class="statement-title">Example.</span> Constant & Linear<br>

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/non-parametric-1.jpg" | relative_url }}" width="450px">
</div>

$f_i$를 constant function, linear function으로 모델링 했을 때의 결과이다. 그림에서도 볼 수 있듯이 <span class="half_HL">knots 주변에서 continuous 하지 않다</span>.

<hr/>

### Regression Spine

<span class="statement-title">Definition.</span> Regression Polynomial Spline<br>

Given a fixed knot sequence $\xi_1, \dots, \xi_K$,, a function defined on an open interval $(a, b)$ is called a \<**<u>regression (polynomial) spline of order $M$</u>**\> if it is a piecewise polynomial of order $M$ on each of the intervals.

$$
(a=\xi_0, \xi_1], (\xi_1, \xi_2], \dots, (\xi_k , b=\xi_{k+1})
$$

and <span class="half_HL">has continuous derivatives up to order $(M-1)$</span>.

앞에서 살펴본 \<Local Polynomial Regression\>의 not-continuous 문제를 해결하기 위해 \<Regression Spline\>에서는 piecewise polynomial이 $(M-1)$차 연속인 도함수를 가져야 한다는 조건이 추가된 것이다!!

<br/>
<hr/>

<span class="statement-title">Example.</span> 3rd-order polynomial ($M=3$)<br>

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/non-parametric-2.jpg" | relative_url }}" width="500px">
</div>

왼쪽은 앞에서 살펴본 \<Local polynomial regression\>의 모델이다. knot에서 not-continuous하다.

오른쪽은 <span class="half_HL">knot에서 continuous해야 한다</span>는 제약을 준 모델이다.

이는 $x \mapsto a_3 x^3 + a_x x^3 + a_1 x + a_0$인 각 $f_i\left((\xi_{i-1}, \xi_i]\right)$에 대해 

$$
f_i(\xi_i) = f_{i+1}(\xi_i)
$$

라는 조건이 추가된 것이다. 이는 곧, $f_i(\xi_i) = f_{i+1}(\xi_i)$이기 때문에, $f_{i+1}$에서 $b_4, b_3, b_2$에 대한 값이 정해졌다면, 자동으로 $b_0$의 값이 결정된다.

$$
a_3 x^3 + a_2 x^2 + a_1 x + a_0 = b_3 x^3 + b_2 x^2 + b_1 x + \cancelto{\text{calculated by contraint}}{b_0}
$$

따라서, estimate 해야 하는 Coefficients의 갯수는

$$
(M+1)(K+1) - (K-1)
$$

(ex: If $M=3$ and $K=2$, then we need to estimate $4 + 4 - 1$ coefficients.)

<br/>
<hr/>

<span class="statement-title">Example.</span> 3rd-order polynomial with 1st & 2nd derivative<br>

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/non-parametric-3.jpg" | relative_url }}" width="500px">
</div>

이번에는 "knot에서 continuous" 조건과 함께 "<span class="half_HL">knot에서 1st/2nd derivatives continuous</span>" 조건이 추가되었다.

이를 만족하려면, $f_i' (\xi_i) = f_{i+1}'(\xi_i)$를 만족해야 하며, 이것은 곧

$$
3 a_3 x^2 + 2 a_2 x + a_1 = 3 b_3 x^2 + 2 b_2 x + \cancelto{\text{calculated by contraint}}{b_1}
$$

이므로 contraint를 통해 $b_1$의 값을 정할 수 있다는 말이 된다. 2nd derivative continuous에 대해서도 동일한 방법으로 접근하면 된다.

따라서, estimate 해야 하는 Coefficients의 갯수는

$$
(M+1)(K+1) - MK = M + K + 1
$$

<br/>
<hr/>

#### Spline basis function

<span class="statement-title">Notation.</span><br>

$$
x_{+} = \begin{cases}
    x & \text{if} \quad x > 0 \\
    0 & \text{else}
\end{cases}
$$

또는

$$
(x-\xi)_{+}^M = \begin{cases}
    (x-\xi)^M & \text{if} \quad x > \xi \\
    0 & \text{else}
\end{cases}
$$

<span class="statement-title">Example.</span><br>

만약 $M=1$(linear) and $K=2$라면, **spline basis function**은 아래와 같다.

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/spline-basis-function-1.jpg" | relative_url }}" width="500px">
</div>

<br/>

만약 $M=3$(cubic) and $K=2$라면, **spline basis function**은 아래와 같다.

<div class="img-wrapper">
  <img src="{{ "/images/statistical-data-mining/spline-basis-function-2.jpg" | relative_url }}" width="500px">
</div>

<hr/>

### Natural Cubic Spline

완벽할 것 같은 \<Regression Spline\> 방식도 작은 문제를 가지고 있다. 바로 양끝 boundary에서 regression이 잘 안 된다는 것이다. 이를 위해 \<Natural cubic spline\>은 <span class="half_HL">양끝에서 linear로 모델링 한다<span>.

<span class="statement-title">Definition.</span> Natrual Cubic Spline<br>

A cubic spline is called a \<**natural cubic spline**\> if it is **linear** beyond the boundary knots $\xi_1$ and $\xi_K$.

<div class="img-wrapper">
  <img src="http://www.stanford.edu/class/stats202/figs/Chapter7/7.7.png" width="500px">
    <p>
  (출처: <a href="http://web.stanford.edu/class/stats202/notes/Nonlinear/Splines.html">Stanford - STAT202</a>)
  </p>
</div>

그림에서 볼 수 있듯이 높은 차원의 $M$으로 근사할 수록 \<Regression Spline\>은 boundary에서 성능이 저하되는 걸 볼 수 있다.




