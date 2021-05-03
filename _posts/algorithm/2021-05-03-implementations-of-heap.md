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

- heap by unordered array
- heap by ordered array
- binary heap
- d-ary heap
- Fibonacci heap

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




<hr/>

#### 참고자료

- ['핑크마구로'님의 포스트](https://algs4.tistory.com/48)
  - PQ에 대한 문제와 PQ를 이용한 \<A* Algorithm\> 다양한 내용의 포스트가 있다 👍
- [geeksforgeeks: K-ary Heap](https://www.geeksforgeeks.org/k-ary-heap/)
- [Wikipedia: d-ary heap](https://en.wikipedia.org/wiki/D-ary_heap)