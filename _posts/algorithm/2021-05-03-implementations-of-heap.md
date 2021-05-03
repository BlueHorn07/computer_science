---
title: "Implementations of Heap"
layout: post
use_math: true
tags: ["Algorithm"]
---

### 서론

이 포스트는 위키피디아의 [Heap(data structure)](https://en.wikipedia.org/wiki/Heap_(data_structure))에 소개된 Heap의 구현들을 다룹니다. 지적과 조언은 언제나 환영입니다 ㅎㅎ

이번 포스트에서는 \<Heap\>의 구현 방식을 살펴볼 예정입니다. 구현 코드는 별도의 포스트에서 구현 방식 별로 추후에 다룰 예정입니다! 😁

<hr/>

\<Priority Queue\>의 구현인 \<Heap\>은 많은 알고리즘에서 핵심적인 역할을 한다. 보통 Binary Tree로 구현하는 \<Binary Heap\>을 많이 알테지만, 정규 수업이나 위키피디아의 문서를 살펴보면 \<Binary Heap\> 외에도 여러 형태의 \<Heap\>에 대한 구현이 존재한다!! 이번 포스트에선 이 \<Heap\>의 구현에 대해 자세히 알아볼 예정이다. 😎

- Heap by unordered array
- Heap by ordered array
- [Binary Heap]({{"/2021/05/03/implementations-of-heap.html#binary-heap" | relative_url}})
- [d-ary Heap]({{"/2021/05/03/implementations-of-heap.html#d-ary-heap" | relative_url}})
- [Binomial Heap]({{"/2021/05/03/implementations-of-heap.html#binomial-heap" | relative_url}})
  - Binomial Tree
- [Fibonacci Heap]({{"/2021/05/03/implementations-of-heap.html#fibonacci-heap" | relative_url}})

<hr/>

### Unodered Array & Ordered Array

min 또는 max에 빈번히 접근하는 priority queue를 배열로 naive 하게 구현하는 방식이다. 정말 아무런 테크닉을 사용하지 않았기 때문에 쿼리가 들어올 때마다 linear search 또는 binary search를 통해 쿼리를 해결한다.

<br><span class="statement-title">Unordered Array.</span><br>

- $\texttt{getMin}$: $O(N)$
  - 선형 탐색으로 min 찾아서 리턴
- $\texttt{insert}$: $O(1)$
  - 그냥 배열의 맨 뒤에 붙이면 OK
- $\texttt{deleteMin}$: $O(N)$
  - 선형 탐색으로 min 찾음 $O(N)$
  - 배열이므로 삭제에 $O(N)$ 소요

<br><span class="statement-title">Ordered Array.</span><br>

원소가 하나 추가될 때마다 정렬해 Ordered 구조를 유지. 이때, min-heap이라면, min이 배열 맨 끝에 있는 구조여야 한다. <small>// 그 이유는 min이 배열 맨 앞에 있게 되면, $\texttt{deleteMin}$에서 손해임. 직접 비교해보면 금방 이해가 된다.</small>

- $\texttt{getMin}$: $O(1)$
  - 맨 뒤에 있는 min 원소를 리턴
- $\texttt{insert}$: $O(N)$
  - 이진 탐색으로 자신의 위치를 찾음 $O(\log N)$. 
  - 배열이므로 삽입에 $O(N)$ 소요.
- $\texttt{deleteMin}$: $O(1)$
  - 맨 뒤에 있는 min 원소를 삭제. 맨 뒤의 원소를 없애므로, $O(1)$

<hr/>

### Binary Heap

일반적으로 배우는 \<Heap\> 자료구조이다. \<완전 이진 트리; Complete Binary Tree\>라는 트리 구조로 구현된다. 사실 완전 이진 트리라고 별게 있는게 아니라 배열로 구현된 Binary Tree에서 부모-자식 사이의 관계가 

- 부모 → 자식: $k$ → ($2k$ & $2k+1$)
- 자식 → 부모: $k$ → $k/2$

인 구조일 뿐이다. 다만, 이 구조일 때, \<heapify\>라는 \<Heap\>의 연산을 $O(\log N)$의 시간으로 효율적으로 수행할 수 있기 때문에 \<Heap\>의 구현으로 자주 소개된다. 물론 이런 배열로 구현하지 않고, 평범한 트리 형태로 구현해도 동일한 효율을 보인다.

<div class="statement">

<span class="statement-title">Heap-Order.</span><br>

부모 노드의 키가 자식 노드의 키보다 항상 크거나 같다.

</div>

\<Binary Heap\>에서의 $\texttt{insert}$와 $\texttt{deleteMin}$는 루트 노드에서 말단 노드까지 또는 그 반대 방향으로 $\texttt{swim}$ & $\texttt{sink}$ 연산을 수행하는 것으로 이루어진다.

$\texttt{swim}$은 부모 노드보다 큰 key를 가진 자식 노드가 부모 노드와 swap 되어 루트 노드 쪽으로 올라가는 것을 말한다.

$\texttt{sink}$는 자식 노드보다 작은 key를 가진 부모 노드가 자식 노드와 swap 되어 말단 노드 쪽으로 내려가는 것을 말한다.

이번 포스트에서 \<Binary Heap\>에 대해 간단히 소개만 하고, 동작과 구현을 자세히 논하지는 않겠다. 추후에 \<Binary Heap\>의 구현 코드에서 좀더 자세히 다루고, 지금은 Time Complexity 위주로 살펴보겠다.

- $\texttt{getMin}$: $O(1)$
  - 루트 노드를 리턴
- $\texttt{insert}$: $O(\log N)$
  - 최악의 경우, \<Heap\>의 깊이 만큼 $\texttt{swim}$ 연산을 수행.
  - Complete Binary Tree이기 때문에 깊이 $D$는 $O(\log N)$이다 → $O(\log N)$
- $\texttt{deleteMin}$: $O(\log N)$
  - 맨 뒤 원소를 루트로 swap 후, 루트 노드 였던 것을 삭제
  - 최악의 경우, \<Heap\>의 깊이 만큼 루트 노드에서부터 $\texttt{sink}$ 연산을 수행 → $O(\log N)$

<hr/>

### d-ary Heap

\<d-ary Heap\>은 <span class="half_HL">\<Binary Heap\>의 generalization</span>이다. \<Binary Heap\>은 각 노드가 2개의 자식 노드를 가졌다면, \<d-ary Heap\>은 각 노드가 d개의 자식 노드를 가지는 Complete Tree이다. 따라서, \<Binary Heap\>은 $d=2$인 특수한 경우라고 볼 수 있다.

\<d-ary Heap\>의 동작은 \<Binary Heap\>의 동작과 동일하다. 각 노드는 **<u>Heap Order</u>**를 만족해야 하며, **<u>Heapify</u>**를 통해 Heap을 구성한다. 다만, 자식 노드의 수가 많아져, Heap의 깊이 $D$가 $\log_d N$으로 얕아 졌다. 이에 따라 각 연산의 Time Complexity는 아래와 같이 유도된다.

- $\texttt{getMin}$: $O(1)$
  - 루트 노드를 리턴
- $\texttt{insert}$: $O(\log_d N)$
- $\texttt{deleteMin}$: $O(d \log_d N)$

<div class="math-statement" markdown="1">

<b>\* $\texttt{deleteMin}$ in d-ary Heap</b>

먼저 $d=2$인 Binary Heap의 경우를 살펴보자. 만약 현재 min-Heap이 아래와 같이 구성되어 있다면,

<pre>
   3       2       1
  / \  →  / \  →  / \
  2 1     3 1     3 2
</pre>

와 같은 방식으로 최대 2번 $\texttt{Heapify}$를 호출한다.

이번에는 $d=3$인 경우를 살펴보자. 만약 현재 min-Heap이 아래와 같이 구성되어 있다면,

<pre>
    4         3         2         1
  / | \  →  / | \  →  / | \  →  / | \
 3  2  1   4  2  1   4  3  1   4  3  2
</pre>

와 같은 방식으로 최대 3번의 $\texttt{Heapify}$를 호출한다.

각 $\texttt{Heapify}$는 $O(\log_d N)$의 시간이 소요되므로, $\texttt{deleteMin}$은 $O(d \log_d N)$의 시간이 소요된다.

</div>

ps) $d=3$인 d-ary Heap을 \<Ternary Heap\>이라고도 부른다.

💥 Wikipedia에 기술된 내용에 따르면, 실전에서는 \<4-ary Heap\>이 $\texttt{deleteMin}$ 시간복잡도에서 열세임에도 불구하고, \<Binary Heap\> 보다 더 좋은 성능을 낸다고 한다. 그 이유는 \<4-ary Heap\>이 \<Binary Heap\>보다 Cache에서 더 이득을 보기 때문이라고 한다 😁

<hr/>

### Binomial Heap

\<Binomial Heap\>은 <span class="half_HL">서로 다른 두 Heap을 병합(merge)해 새로운 Heap을 구성하는 것에 특화된 Heap 구조</span>다. 

\<Binomial Heap\>은 **\<Binomial Tree\>**라는 특별한 형태의 트리의 집합으로 구성된다. 먼저 \<Binomial Tree\>에 대해 살펴본 후, \<Binomial Heap\>에 대해 살펴보겠다. 이번 포스트의 내용은 아래 유튜브 영상의 내용을 적절히 정리한 것임을 미리 밝힌다.

<div align="center">
<iframe width="450" height="300" src="https://www.youtube.com/embed/m8rsw3KfDKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

#### Binomial Tree

<div class="img-wrapper">
  <img src="{{ "/images/algorithm/binomial-tree-1.jpg" | relative_url }}" width="500px">
</div>

\<Binomial Tree\>는 <span class="half_HL">degree가 같은 두 \<Binomial Tree\>를 병합(merge)함으로써 구축</span>한다. 방법은 그렇게 어렵지 않고, 아래의 예시를 보면 바로 이해 될 것이다. 😊

<pre>
(deg 0)   (deg 0)       (deg 1)       |    (deg 1)   (deg 1)       (deg 2)
   4    +    10     →       4         |       1    +    7     →       1
                            |         |       |         |           / |
                            10        |       9         15         7  9 
                                      |                            |
                                      |                           15
</pre>


\<Binomial Tree\>는 아래의 4가지 성질을 만족한다.

1\. degree $k$의 \<Binomial Tree\>의 루트 노드는 정확히 $k$개의 자식 노드를 갖는다.

2\. degree $k$의 \<Binomial Tree\>는 정확히 $2^k$개의 노드와 깊이 $k$를 갖는다.

3\. \<Binomial Tree\>의 루트 노드는 degree $k-1$, $k-2$, ..., $0$의 Binomial Tree를 자식으로 갖는다.

4\. degree $k$의 \<Binomial Tree\>에서 depth $d$를 갖는 노드의 수는 $\displaystyle\binom{k}{d}$이다. 이 성질 때문에 \<Binomial Tree\>라는 이름이 붙었다 😎

#### Binomial Heap

<div class="img-wrapper">
  <img src="{{ "/images/algorithm/binomial-heap-1.jpg" | relative_url }}" width="300px">
</div>

다시 \<Binomial Heap\>으로 돌아오자. \<Binomial Heap\>은 아래의 조건에 따라 모인 \<Binomial Tree\>의 집합이다.

1\. Heap을 구성하는 각 Binomial Tree는 Heap Order를 따른다.

2\. degree 0을 포함해 각 order별로 0개 또는 1개, 즉 각 order별 최대 1개의 이항 트리가 Heap에 존재한다.

2번재 조건은 전체 $n$개 노드가 존재할 때, \<Binomial Heap\>이 최대 $(1 + \log n)$개의 이항 트리로 구성됨을 말한다. 또한, Heap에 존재하는 각 Binomial Tree의 degree는 **<u>유일하게</u>** 결정된다. 전체 노드의 수 $n$을 이진수로 표현한다면, 각 digit은 Heap에 존재하는 Binomial Tree의 갯수를 의미한다. 따라서, 전체 노드 수 $n$에 대해 Binomial Heap의 구성은 유일하다! 💥

<br><span class="statement-title">장점.</span> Fast Heap Merge<br>

<div class="img-wrapper">
  <img src="https://t1.daumcdn.net/cfile/tistory/2364044258AC61FA35" width="500px">
</div>


<hr/>

### Fibonacci Heap


<hr/>

#### 참고자료

- ['핑크마구로'님의 포스트](https://algs4.tistory.com/48)
  - PQ에 대한 문제와 PQ를 이용한 \<A* Algorithm\> 등 다양한 내용의 포스트가 있습니다 👍
- [geeksforgeeks: K-ary Heap](https://www.geeksforgeeks.org/k-ary-heap/)
- [Wikipedia: d-ary heap](https://en.wikipedia.org/wiki/D-ary_heap)
- ['Jeff Zhang'님의 유튜브 영상](https://www.youtube.com/watch?v=m8rsw3KfDKs) - Binomial Heap