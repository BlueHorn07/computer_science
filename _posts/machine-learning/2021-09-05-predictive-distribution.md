---
title: "Predictive Distribution"
layout: post
use_math: true
tags: ["Machine Learning"]
---

### 서론

"Machine Learning"을 공부하면서 개인적인 용도로 정리한 포스트입니다. 지적은 언제나 환영입니다 :)

<div class="proof" markdown="1">

**Bayesian Approach**

1. [MLE vs. MAP]({{"/2021/09/05/MLE-vs-MAP.html" | relative_url}})
2. [Predictive Distribution]({{"/2021/09/05/predictive-distribution.html" | relative_url}}) 👀
3. Bayesian Regression

</div>

<hr/>

## Bayesian Approach

이번 포스트부터 본격적으로 Bayesian Approach에 대해 탐구한다. 먼저 Bayesian의 관점에서는 확률(probability)을 <span class="half_HL">"가설에 대한 믿음의 정도"</span>로서 이해한다. 그래서 사전 믿음을 가지고 가설을 살펴보고, 이후에 데이터를 관측했다면 그 데이터를 가지고 새롭게 믿음을 갱신해 사후 믿음을 얻는다. 이런 수집-갱신의 과정을 데이터가 발생할 때마다 계속 반복한다.

기억할 점은 Bayesian Approach는 항상 '불확실성(uncertainty)'에 대해 얘기한다는 것이다. 고전적인 확률론이 **Point Estimation**으로 unbiased estimator 또는 the most efficient estimator of $\theta$ (= unbiased estimaor with the smallest variance)를 구하거나 또는 **Interval Estimation**으로 confidence level을 구하는 등의 추정을 수행하지만, Bayesian Approach는 parameter $\theta$에 대한 <b><span style="color: red">'확률 분포'</span></b>를 찾는 것을 목표로 한다. 그래서 Point Estimation에서 처럼 parameter의 값을 $\theta = \theta_0$로 특정하는 것이 아니라 "$\mu = 4$, $\sigma^2 = 1$인 정규분포로 parameter가 분포되어 있다"라고 말한다.

<span class="half_HL">Bayesian Approach에서는 관측 데이터가 추가됨에 따라 parameter의 distribution을 계속 갱신한다.</span> 이는 parameter의 prior distribution을 새롭게 관측된 데이터로 갱신해 posterior distribution을 얻는 셈이다. [이 아티클](https://coffeewhale.com/bayesian/linear/regression/2019/10/19/bayesian-lr/)에서는 이것을 데이터가 확률 분포를 잡아당기는 자석과 같다고 표현하는데, 그 표현이 그럴싸 하다 😲 자세한 내용은 해당 아티클의 [요 부분](https://coffeewhale.com/bayesian/linear/regression/2019/10/19/bayesian-lr/#:~:text=%EC%A0%80%EB%8A%94%20%EC%9D%B4%EA%B2%83%EC%9D%84%20%EB%8B%A4%EC%9D%8C%EA%B3%BC%20%EA%B0%99%EC%9D%B4%20%ED%91%9C%ED%98%84%ED%95%98%EA%B8%B8%20%EC%A2%8B%EC%95%84%ED%95%A9%EB%8B%88%EB%8B%A4.)을 잠깐 읽어보고 오는 걸 추천한다. 글을 통해 데이터가 posterior distribution을 어떻게 갱신하는지 그리고 prior distribution을 잘 잡는게 중요한 이유를 깨달을 수 있다 👍

기존의 고전적인 방법은 Point Estiamtor나 confidence interval를 유도했다. 그러나 Bayesian Approach에서는 그런 것들이 전혀 없으며👋 단지 paramter에 대한 **posterior distribution**을 이용해 새로운 데이터 $x^{*}$에 대해 예측할 뿐이다. 그리고 이 과정에서 등장하는 것이 바로 \<**Predictive Distribution**; 예측 분포\>이다!

<hr/>

## Parameter Posterior

앞의 문단에서 Bayesian Approach가 관측 데이터로 parameter의 distribution을 갱신한다고 기술했다. 이것을 좀더 살펴보자! 제일 먼저 parameter $\theta$에 대한 prior distribution을 가정한다. 이것을 \<prior distribution of parameter\> 또는 \<parameter prior\>라고 하며, 여기서는 아래와 같은 정규 분포를 가정하겠다.

$$
\theta \sim N(0, \tau^2 I)
$$

이제 관측된 데이터 $S = (X, y)$가 존재해 이것으로 \<parameter prior\>를 갱신해보자. 그러면 Bayes Rule을 이용해 아래와 같이 \<parameter posterior\>를 유도할 수 있다.

$$
\begin{aligned}
p(\theta \mid S)
&= \frac{p(S \mid \theta) p(\theta)}{p(S)} = \frac{p(S \mid \theta) p(\theta)}{\int_{\theta'} p(S \mid \theta') p(\theta') d\theta'} \\
&= \frac{p(\theta) \prod^m_{i=1} p(y^{(i)} \mid x^{(i)}, \theta)}{\int_{\theta'} p(\theta') \prod^m_{i=1} p(y^{(i)} \mid x^{(i)}, \theta') d\theta'}
\end{aligned}
$$



<hr/>

## Predictive Distribution

휴! \<Predictive Distribution; 예측 분포\>를 소개하기까지 오랜 시간이 걸렸다. 우리는 고전적인 방법에 너무 익숙해져 있기 때문에 이 녀석을 잘 이해하려면 <span class="half_HL">**Bayesian Approach**가 고전적인 방법과 어떻게 다른지를 이해</span>하고 <span class="half_HL">고전적인 방법의 estimator와 confidence interval 등의 개념들을 폐기~~는 아니고 Bayesian에서는 쓰지 않는다 정도로 이해하면 된다~~</span>해야 함을 인지해야 한다고 생각한다.

\<Predictive Distribution\>은 observed data $S = (X, y)$(train-set)와 unobserved data $S^{\*} = (X^{\*}, y^{\*})$(test-set)가 있을 때, unobserved data $x^{\*} \in X^{\*}$에 대한 prediction을 수행하는 과정에서 유도하는 분포이다. 그래서 이름에 "predictive"라는 이름이 붙었다고 할 수 있다. ~~뇌피셜입니다~~ \<Predictive Distribution\>은 prior distribution으로 유도하는지, posterior distribution으로 유도하는지에 따라 두 가지로 나뉜다.

<div class="definition" markdown="1">

<span class="statement-title">Definition.</span> Prior Predictive Distribution<br>

Let $S = \\{ (X, y) \\}$ be a set of observed data, $X^{\*}$ be a set of unobsersed data, and $x^{\*} \in X^{\*}$.

Then, the \<prior predictive distribution\> is

$$
p(y \mid x) = \int p(y, \theta \mid x) d\theta = \int p(y \mid x, \theta) p(\theta) d\theta
$$

즉, paramter의 prior distribution $p(\theta)$와 $y$에 대한 likelihood $p(y \mid x, \theta)$의 곱을 적분한 것이 prior predictive distribution이다. likelihood에 대해 좀더 구체적으로 말하면 $\theta$를 paramter로 한 분포들: 이항 분포, 정규 분포 등등이라고 생각하면 된다. 그리고 likelihood는 데이터가 어떤 분포로 추출될 것이라고 <span style="color: red">가정</span>하는 것에서 비롯된다는 점도 구분하자.

ex)

$$
p(y^{(i)} \mid x^{(i)}, \theta) = \frac{1}{\sqrt{2\pi} \sigma} \exp \left( - \frac{(y^{(i)} - \theta^T x^{(i)})^2}{2\sigma^2}\right)
$$

</div>

그러나 위의 식을 보면 observed data $S$에 대한 정보는 전혀 없다. 그래서 데이터를 제대로 활용하려면 observed data $S$로 갱신한 posterior distribution인 $p(\theta \mid S)$로 유도한 \<posterior predictive distribution\>을 사용해야 한다!

<div class="definition" markdown="1">

<span class="statement-title">Definition.</span> Posterior Predictive Distribution<br>

$$
p(y \mid x, S) = \int p(y, \theta \mid x, S) d\theta = \int p(y \mid x, S, \theta) p(\theta \mid S) d\theta
$$

보통 $x^{\*}$와 $S$를 독립이라고 가정하기 때문에 또는 iid를 가정하기 때문에 이것을 적용하면,

$$
p(y \mid x, S) = \int p(y \mid x, S, \theta) p(\theta \mid S) d\theta = \int p(y \mid x, \theta) p(\theta \mid S) d\theta
$$

후! 식이 훨씬 간단해졌다! prior predictive distribution과 비교했을 때 달라진 점은 적분 내부의 함수가 prior distribution에서 posterior distribution으로 바뀌었다는 점이다! 이것은 posterior predictive distribution은 관측된 데이터로 갱신된 posterior distribution을 사용했기 때문에 실제 모수(parameter)와 근접할 것으로 기대되는 정보를 바탕으로 예측(prediction)했다고 기대하게 된다!

</div>

[이 아티클](https://rooney-song.tistory.com/9?category=935544/#:~:text=문제)의 해당 부분에서 predictive distribution을 유도하는 간단한 예제를 풀어볼 수 있다. 문제가 좋으니 한번쯤 풀어보도록 하자 👀 참고로 첫번째 예제에서 Gamma function $\Gamma$를 써서 적분하는 부분은 [Beta Distribution](https://bluehorn07.github.io/mathematics/2021/04/06/chi-and-beta-and-lognormal-distribution.html#beta-distribution)에 대한 적분이다.

<hr/>

그럼 \<Predictive Distribution\>은 어떻게 쓰는 것인가? 다음 포스트에서 다루는 Bayesian Regression에서 그 의문을 해소할 수 있다! 스포를 하자면 \<Posterior Predictive Distribution\>를 구하는 것이 Bayesian Regression의 목표다!

<hr/>

### reference

- [[번역] 선형 회귀 모델 Bayesians vs Frequentists](https://coffeewhale.com/bayesian/linear/regression/2019/10/19/bayesian-lr)
- [Prior & Posterior Predictive Distributions](https://donghwa-kim.github.io/Pred_-baye.html)
- [사전예측분포와 사후예측분포(Prior and posterior predictive distribution)](https://rooney-song.tistory.com/9?category=935544)
- [](https://medium.com/jun-devpblog/bayesian-dl-1-properties-of-gaussian-distribution-and-prior-posterior-predictive-distribution-b02529b894a8)