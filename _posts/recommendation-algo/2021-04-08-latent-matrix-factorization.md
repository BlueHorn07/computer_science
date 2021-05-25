---
title: "Latent Matrix Factorization"
layout: post
use_math: true
tags: ["Recommendation Algorithm"]
---

### 서론
2021-1학기, 대학에서 '과제연구' 수업에서 진행하는 개인 프로젝트를 위해 개인적으로 정리한 포스트입니다. 지적과 교류는 언제나 환영입니다 :)

<br><span class="statement-title">TOC.</span><br>

- Model Design 
- How to Trian?: Loss

<hr/>

### Model Design

<div class="img-wrapper">
  <img src="https://t1.daumcdn.net/cfile/tistory/99A2523D5C910CD90B" width="400px">
  <p>
  (출처: <a href="https://yeomko.tistory.com/5?category=805638">갈아먹는 추천 알고리즘</a>)
  </p>
</div>

먼저 셋업을 좀 살펴보자.

행렬 $R \in \mathbb{R}^{N_u \times N_i}$은 평점 행렬로, 각 유저가 아이템에 대해 매긴 평점 정보가 들어있다. 이때, $N_u$는 총 유저의 수, $N_i$는 총 아이템의 수를 의미한다.

이제 이 행렬 $R$를 \<latent factor matrix\> $X$, $Y$로 분해해보자! <span class="half_HL">이때 "**latent factor의 차원**"을 정해야 하는데, $N_f$라고 설정해두자!</span> 보통 50에서 200 사이로 설정한다고 한다. 그래서 MF를 진행하면, 행렬 $X$, $Y$는 각각 $X \in \mathbb{R}^{N_f \times N_u}$, $Y \in \mathbb{R}^{N_f \times N_i}$가 된다. 

\<Latent factor matrix\> $X$, $Y$는 각각 우리가 학습시키고자 하는 대상이다. 이 행렬들은 처음에 아주 작은 랜덤값으로 초기화된다. <small>(💥 행렬 $R$의 값을 쪼개어 생성하는 것이 아니다!)</small>

<div class="img-wrapper">
  <img src="https://t1.daumcdn.net/cfile/tistory/990FBA3A5C910D0A1A" width="400px">
  <p>
  (출처: <a href="https://yeomko.tistory.com/5?category=805638">갈아먹는 추천 알고리즘</a>)
  </p>
</div>

이제 우리는 factor matrix $X$, $Y$를 통해 평점 행렬의 prediction인 $\hat{R}$을 유도할 것이다. 방법은 간단한데, 그냥 $X$와 $Y$를 곱해주면 된다.

$$
\hat{R} = X^T \times Y
$$

이때, 행렬 $\hat{R}$에서 entry $\hat{r}_{ui}$는 유저 $u$가 아이템 $i$에 대해 내리는 평점을 prediction한 것이다. 

$$
\hat{r}_{ui} = x_u^T \times y_i
$$

즉, 사용자의 latent vector $x_u$와 아이템의 latent vector $y_i$를 곱해 평점을 추론하는 것이다. 그래서 <span class="half_HL">LMF 모델의 목표는 $$\hat{r}_{ui}$$가 최대한 $$r_{ui}$$와 가까워지도록 Latent Factor Matrix $$X$$, $$Y$$의 값을 조정하는 것이라고 보면 된다!</span>

<hr/>

### How to Trian?: Loss

이제 모델을 학습시키기 위한 파트다. 방법은 strightforward 한데, 그냥 $\hat{r}_ui$와 $r_{ui}$ 사이의 값이 가까워지도록 두 값의 차이값을 minimize 하면 된다!

$$
L(X, Y) = \sum_{u, i} \left( r_{ui} - x_u^T y_i \right)^2
$$

Regularization 텀을 추가해주면 아래와 같다.

$$
L(X, Y) = \sum_{u, i} \left( r_{ui} - x_u^T y_i \right)^2 + \lambda \left( \sum_u \left| x_u \right|^2 + \sum_i \left| y_i \right|^2 \right)
$$

<hr/>

### Optimization

Loss Function을 디자인 했으니 이제 Optimization만 달성하면 된다. 두 가지 방법이 있는데, \<**Graident Descent**\>와 \<**Alternating Least Squares**\>, 두 가지 알고리즘이 있다. 각각 어떻게 동작하는지 살펴보자!

#### Gradient Descent

GD는 그냥 Loss 함수 $L(X, Y)$를 미분하고 이에 대한 Gradient 값을 back-propagation 해주면 된다. 실제 동작은 딥러닝 프레임워크를 사용하면 쉽게 달성할 수 있다.

간단하게 $x_u$에 대해서만 GD를 적용해보겠다.

$$
\begin{aligned}
\frac{\partial}{\partial x_u} L(x_u, y_i) &= \frac{\partial}{\partial x_u} \left( \sum_i \left( r_{ui} - x_u^T y_i \right)^2  + \lambda \left( \left| x_u \right|^2 + \sum_i \left| y_i \right|^2 \right)\right) \\
&= \sum_i 2 \left( r_{ui} - x_u^T y_i \right) (-y_i) + \lambda (2 x_u)
\end{aligned}
$$

이제 이 Gradient 값으로 weight update를 진행하면 된다.

$$
x_u \leftarrow x_u + \alpha \cdot \left( \sum_i \left( r_{ui} - x_u^T y_i \right) (y_i) - \lambda x_u \right)
$$

💥 본인은 $y_i$의 차원 때문에 유도를 하고도 위의 식이 조금 헷갈렸는데, 셋업을 다시 보니까, $y_i$가 $N_f$ 차원의 열벡터였다 ㅋㅋㅋ

Graidnet Descent 방식의 단점은 최적화를 시키는 과정이 너무 느리고, 많은 반복이 필요하면 Global minimum이 아닌 local minum에 stuck할 가능성이 있다 등등의 단점이 있다. ~~단점이 있긴 있다~~ 이런 \<Alternating Least Squares\>는 이런 문제를 스마트하게 해결한다! 😎

#### Alternating Least Sqaures

\<Alternating Least Squares\>의 컨셉은 <span class="half_HL">$X$, $Y$ 둘 중 하나를 고정시키고, 다른 하나를 최적화 시킨다</span>는 것이다. 이 과정을 번갈아가면 반복, 즉 alternating 하면서 짧은 시간 내에 최적의 $X$, $Y$를 찾아낸다!



<hr/>

### references

- [갈아먹는 추천 알고리즘 [3]](https://yeomko.tistory.com/5?category=805638)
- [갈아먹는 추천 알고리즘 [4]](https://yeomko.tistory.com/4?category=805638)
- ['vvakki_'님의 포스트](https://velog.io/@vvakki_/Matrix-Factorization-2)