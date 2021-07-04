---
title: "Gaussian Process & Gaussian Process Regression"
layout: post
use_math: true
tags: ["Machine Learning"]
---

### 서론

"Machine Learning"을 공부하면서 개인적인 용도로 정리한 포스트입니다. 지적은 언제나 환영입니다 :)

<br><span class="statement-title">TOC.</span><br>

- [Gaussian Process](#gaussian-process)
- [Gaussian Process Regression](#gaussian-process-regression)

<hr/>

### Gaussian Process

포스트를 시작하기에 앞서 \<Gaussian Distribution\>에 대해 복습해보자.

**1\. 1D Gaussian Distribution**

$$
f(x) = \frac{1}{\sqrt{2\pi} \sigma} \exp \left( - \frac{(x-\mu)^2}{2\sigma^2}\right)
$$

**2\. 2D Gaussian Distribution**

$$
f(\mathbf{x}) = \frac{1}{2\pi \left| \Sigma \right|^{1/2}} \exp \left( - \frac{1}{2} (\mathbf{x} - \mu)^T \Sigma^{-1} (\mathbf{x} - \mu) \right)
$$

**3\. Multi-variate Gaussian Distribution**

Distribution over random vectors!

$$
f(\mathbf{x}) = \frac{1}{(2\pi)^{n/2} \left| \Sigma \right|^{1/2}} \exp \left( - \frac{1}{2} (\mathbf{x} - \mu)^T \Sigma^{-1} (\mathbf{x} - \mu) \right)
$$

이제 \<Gaussian Process\>의 정의를 살펴보자.

<div class="definition" markdown="1">

<span class="statement-title">Definition.</span> Gaussian Process<br>

A sequence of Gaussian distributions! \<**Gaussian Process**\> is a generlization of the Guassian Distribution. It is a distribution over functions!

$$
\mathcal{GP} (m(x), k(x, x'))
$$

- distribution over functions
  - mean function $m(x)$
  - covariance function $k(x, x')$
- "Every finite subset of RVs in GP is a joint gaussian distribution!"

</div>

이전의 \<Bernoulli Process\>의 경우, 각 trial에서 모두 동일한 \<Bernoulli Distribution\>을 가정했는데, \<Gaussian Process\>의 경우 각 trial의 평균과 분산이 다를 수 있다는 점이 주목할만 하다!

<hr/>

### Gaussian Process Regression

<div class="img-wrapper">
  <img src="https://lh3.googleusercontent.com/-QSlMIVtiVFU/X7SgGoqKYwI/AAAAAAAAOOo/u8vbYa-QeVUW5ppkpHQPQ4hV_CH0vF33wCLcBGAsYHQ/w514-h360/image.png" width="500px">
</div>

앞에서 살펴본 \<Gaussian Process\>를 활용하면, non-parameteric regression을 수행할 수 있다! 😎 "통계적 데이터마이닝(IMEN472)"에서 [non-parameteric model](https://bluehorn07.github.io/computer_science/2021/02/24/statistical-data-mining.html#non-parametric-method)에 대해 다루긴 했는데, \<GP Regression; Gaussian Process Regression\>에 대해서는 다루지 않았다.

\<GP Regression\>은 regression function $f(x)=y$로 GP로 가정해 모델을 만들기 떄문에 mean function $\mu(x)$와 variance function $\sigma(x)^2$를 얻는다. 위의 그림은 regression function $\mathcal{GP}(\mu(x), \sigma(x)^2)$을 바탕으로 regression의 **신뢰구간(confidence level)**을 유도한 것이다. regression의 신뢰구간을 얻을 수 있다는 것은 \<GP Regression\>의 장점 중 하나다! 👍

<br/>

이전의 Parameteric Regression에서는 샘플 데이터 $X$에 대한 최적화 과정을 통해 parameter $\Theta$에 대한 최적해 $\theta$를 유도했다. 이 최적화 과정은 곧 $p(\theta \mid X)$가 최대인 $\theta$를 구하는 것과 같다.

반면에 \<GP Regression\>은 parameter $\Theta$를 <span class="half_HL">probabilistically distributed value</span>로 취급한다. Parameteric Regression에서 $\Theta$를 deterministic value로 취급한 것과는 대조된다. $\Theta$가 RV가 되었기 때문에 이에 대응하는 확률분포 $p(\theta)$도 존재한다.

$$
Y = f(X) + \epsilon
$$

이제 모델의 parameter $\Theta$가 RV가 되었기 때문에 regression model $f(X)$역시 RV가 되며, 어떤 확률 분포를 갖게 된다. 이것을 $p(f \mid X)$라고 하자.

이때, $p(f \mid X)$는 함수에 대한 분포, functional distribution이기 때문에 유도하는 것이 쉽지 않다. 그런데, <span class="half_HL">\<GP Regression\>에서는 regression model $f$가 \<Gaussian Process\>를 따른다고 가정한다!!</span>

$$
p(f) = f(X) \sim \mathcal{GP} \left( \mu(x), k(x, x_i) \right)
$$

이때, mean function, variance function은 아래와 같다.

- $\mu(x) = E [f(x)]$
- $k(x, x') = E \left[(f(x) - \mu(x)) (f(x') - \mu(x')) \right] = \sigma_f^2 \exp \left( - \dfrac{1}{2 L^2} (x - x')^2 \right)$

<br/>

이때 $k(x, x')$는 \<squared exponential kernel\>이다. hyper-parameter로 $\sigma_f$, $L$가 있는데,

- $\sigma_f$: similarity의 크기를 조절
- $L$: similairty 분포의 폭를 조절

$\sigma_f$와 $L$는 \<GP Regression\>의 hyper-parameter로 이 값을 조정해 모델의 bais, variance가 달라진다.

- $L$ 값이 작을수록 가까이 있는 샘플을 주로 본다. 그래서 model의 fluctuation이 심해진다.
  - 극단적으로는 제일 가까이 있는 1 또는 2개 샘플만 보는 경우를 생각해보면 된다.
- 반대로 $L$ 값이 커지면, 멀리 있는 샘플도 반영하기 때문에 model이 smooth 해진다.
- 아래 그림의 첫번째 줄의 경우를 살펴보라.


- $\sigma_f$가 클수록 similarity의 값 자체를 높게 측정하기 때문에, 자연스럽게 model의  variance 값이 커지게 된다.
- 아래 그림의 두번째 줄의 경우를 살펴보라. uncertainty가 존재하는 구역은 매우 큰 uncertainty를 갖는다.

<div class="img-wrapper">
  <img src="https://lh3.googleusercontent.com/-3stFRMVzKRY/X7vwBqAi6GI/AAAAAAAAOxo/pD_ZWUZQ8bg_wk1hnP8QvhMbE-W1cld5QCLcBGAsYHQ/w627-h633/image.png" width="600px">
</div>

<br/>

\<GP Regression\>에서는 mean function $\mu(x)$를 예측 함수로 사용하고, 또 variance function $k(x, x')$를 통해 예측값의 신뢰구간을 구한다.

(사실 \<GP Regression\>을 제대로 이해하려면, 좀더 수학적인 내용과 테크닉을 살펴봐야 한다. 지금은 시간이 없어 이 정도로만 정리하고 넘어가겠다 😥)

<hr/>

어떻게 보면, 다른 non-parametric method인 \<KDE; Kernel Density Distribution\>과도 비슷한 면이 있고, \<KNN\> 기반의 [\<Nadaraya-Watson Estimator\>](https://bluehorn07.github.io/computer_science/2021/05/16/KNN-and-kernel-method.html#nadaraya-watson-estimator)와도 비슷한 면이 있는 것 같다. (셋다 kernel method를 사용하고 있다.) 그래도 \<GP Regression\>은 

- "directly estimate regression function"
- "can report confidence level using variance function"

라는 점에서 두 non-parametric 방법과는 차이가 있는 것 같다.

<hr/>

### references

- ['손쓰'님의 포스트](https://sonsnotation.blogspot.com/2020/11/11-2-gaussian-progress-regression.html)