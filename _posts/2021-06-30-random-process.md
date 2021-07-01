---
title: "Random Process"
layout: post
use_math: true
tags: ["Machine Learning"]
---

### 서론

"Machine Learning"을 공부하면서 개인적인 용도로 정리한 포스트입니다. 지적은 언제나 환영입니다 :)

<hr/>

이번 포스트는 "확률론(Probability Theory)"과 "Machine LEarning"을 공부할 때 등장하는 *"Process"* 가 붙은 모든 개념을 넓은 시야로 살펴보기 위해 작성한 포스트입니다. 다루는 주제는 아래와 같습니다.

- Random Process; Stochastic Process
- Bernoulli Process
- Poisson Process
- Gaussian Process
- Markov Process

<hr/>

## Introduction to Random Process

<div class="definition" markdown="1">

<span class="statement-title">Definition.</span> Random Process<br>

A **random process** is a time-varing function, that assigns the outcome of a random experiment to each time instant.

</div>

대충, (time instant)에 random experiment의 결과(outcome)을 매핑한다는 뜻이다.

또는 아래와 같이 정의하기도 하는데,

<div class="definition" markdown="1">

A (infinite) sequence of random variables $X_1, X_2, \dots, X_n, \dots$

</div>

즉, RV의 infinite sequence를 \<**random process**\>라고 한다. 첫번째 정의보다는 두번째 정의가 좀더 와닿는 편이다. 👍

\<random process\>를 정의할 때, RV $X_i$가 등장했으니 자연스럽게 아래의 성질들을 가질 것이다.

- $E[X_i]$: mean of RV
- $\text{Var}(X_i)$: variance of RV
- $p_{X_i} (x_i)$: marginal probability distribution of RV

우리는 \<random process\> 자체의 분포를 생각해볼 수도 있는데, 이것은 아래와 같은 joint probability distribution이 된다.

$$
p_{X_1, \dots, X_n, \dots} (x_1, \dots, x_n, \dots)
$$

또, 우리는 \<random process\>의 Sample Space $\Omega$에 대해 생각해볼 수 있다.

\<random process\> 중 하나인 \<Bernoulli Process\>의 경우, Sample Sapce는 0-1의 infinite sequence가 된다.

<div class="theorem" markdown="1">

<span class="statement-title">Property.</span> Sample Space of Bernoulli Process<br>

$$
\Omega_{\text{BP}} 
= \left\{ 
  (b_1, \dots, b_n, \dots ) \mid b_i \in \{ 0, 1 \}
  \right\}
$$

</div>

\<Bernoullid Process\>의 경우, Sample Space $\Omega$에서 어떤 subset을 취하는지에 따라 몇가지 Discrete Distribution들을 유도해볼 수 있다! 😁 해당 내용은 아래에서 \<Bernoulli Process\>를 다룰 때, 좀더 소개하겠다.

<hr/>

### Some Properties of Random Process

\<Random Process\>는 아래와 같은 몇가지 특징을 가질 수 있다. <span style="color: red">이것은 필수적인 것은 아니며, 몇몇 \<random process\>에 공통적으로 보이는 특징이거나 가정이다.</span>

<big>**1. Independence btw trials**</big>

개별 trials은 서로 독립적으로 이루어진다. 즉, 영향을 주지 않는다.

- Bernoulli Process, Poisson Process, ...

<big>**2. Memoeryless Property**</big>

$$
P(X = x + k \mid x > k) = P(X = x)
$$

- Bernoulli Process, Poisson Process, ...
- Markov Process

<hr/>

### Bernoulli Process (2)

이 포스트는 \<[Bernoulli Process](https://bluehorn07.github.io/mathematics/2021/03/25/poisson-distribution.html#bernoulli-process)\>에 대한 내용에서 추가적인 주제들을 다룬다. 아직 \<Bernoulli Processs\>가 뭔지 모른다면, 위의 포스트를 먼저 읽어보자!

<div class="theorem" markdown="1">

<big>1. Number of Success $S_n$ in $n$ trials.</big>

Let's derive a random variable $S_n = X_1 + \cdots + X_n$ from the Bernoulli Process.

Then, $S_n$ follows the \<Binomial Distribution\>!

$$
P(S_n = x) = \binom{n}{x} p^x (1-p)^{n-x} \quad \text{for} \; x=0, 1, \dots, n
$$

</div>

<div class="theorem" markdown="1">

<big>2. Time until the first success</big>

Let's derive a randome variable $T_1 = \min \\{ i \in \mathbb{N} : X_i = 1\\}$ from the Bernoulli Process.

Then, $T_1$ follows the \<Geometric Distribution\>!

$$
P(T_1 = x) = P(\underbrace{0, 0, \dots, 0}_{x-1}, 1) = (1-p)^{x-1} p \quad \text{for} \; x=1, 2, \dots
$$

</div>

<div class="theorem" markdown="1">

<big>3. Time until the first $k$ success</big>

\<Geometric Random Variable\>인 $T_1$을 확장한 개념이다. 

Let's derive a randome variable $T_k = \min \\{ i \in \mathbb{N} : \| \\{ X_i : X_i = 1 \\} \| = k\\}$ from the Bernoulli Process.

Then, $T_n$ follows the \<Negative Binomial Distribution\>!

$$
P(T_k = x) = P(\underbrace{0, 1, \dots, 1, \dots, 0}_{k-1 \text{ success}}, 1) = \binom{x-1}{k-1} (1-p)^{x-k} p^k \quad \text{for} \; x=k, k+1, \dots
$$

</div>

<hr/>

### Poisson Process

아래 포스트의 내용으로 대체

👉 [Poisson Process](https://bluehorn07.github.io/mathematics/2021/03/25/poisson-distribution.html#poisson-process)

<hr/>

### Gaussian Process

추후 작성 예정

<hr/>

### Markov Process

추후 작성 예정

<hr/>

### references

- [[MIT OCW] Introduction to Probability: Lecture 21](https://ocw.mit.edu/resources/res-6-012-introduction-to-probability-spring-2018/part-iii-random-processes/MITRES_6_012S18_L21AS.pdf)



