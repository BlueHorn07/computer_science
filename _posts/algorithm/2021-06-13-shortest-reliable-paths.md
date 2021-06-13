---
title: "Shortest Reliable Paths"
layout: post
use_math: true
tags: ["Algorithm"]
---

### 서론

2020-1학기, 대학에서 '알고리즘' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<hr/>

주어진 그래프 $G$에서 최대 $k$개의 edge를 거쳐 노드 $s$에서 노드 $t$로 가는 shortest path를 찾고 싶다. 이전의 \<Dijkstra Algothm\>의 상황과 비슷하지만, <span class="half_HL">최대 $k$개의 edge를 거친다는 조건이 추가</span>된 문제다! 예를 통해 살펴보면, 아래 그래프에서 $T$에서 $B$로 갈 떄, 최대 $1$개의 edge만 거칠 수 있다면, 비용이 $4$인 edge를 거쳐서 도착해야 한다. 이것은 "at most $k$ edge"라는 조건 떄문에 the shortest path인 $(T, D, B)$의 비용 $2$보다 더 큰 비용을 지불하게 된 것이다!

<div class="img-wrapper">
  <img src="{{ "/images/algorithm/shortest-reliable-path-1.png" | relative_url }}" width="300px">
</div>

이 문제는 \<DP\>로 아주 간단하게 풀 수 있다!! 간단하게, 시작노드 $s$에서 각 노드 $v$에 도달할 때의 edge 수를 기록하면 된다!!

<div class="math-statement" markdown="1">

Let $\text{dist}(v, i)$ be the shortest path from $s$ to $v$ that uses $i$ edges. 

(Initialize) set $\text{dist}(v, 0) = \infty$ and $\text{dist}(s, *) = 0$.

Then,

$$
\text{dist}(v, i) = \min_{(u, v) \in E} \left\{ \text{dist}(u, i-1) + \ell(u, v) \right\}
$$

</div>

먼저 시작노드 $s$에서부터 알고리즘을 생각해보자. 그러면, 

<div align="center" markdonw="1">

for a nodes $v$ with $(s, v) \in E$, $\text{dist}(v, 1) = \ell(s, v)$

</div>

가 성립할 것이다.

그 다음은 $s$와 인접한 노드였던 $v$들에 대해 그들의 인접 노드를 찾아 $\text{dist}(u, 2)$에 대해 갱신해준다. 어느 정도는 \<BFS\> 알고리즘과도 비슷한 측면이 있다!

<hr/>

#### 추천 문제

안타깝게도 백준에서 관련된 문제를 찾지 못 했다 😥


