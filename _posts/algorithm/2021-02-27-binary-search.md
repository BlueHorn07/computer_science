---
title: "Binary Search"
layout: post
use_math: true
tags: ["Algorithm"]
---

### 서론
2020-1학기, 대학에서 '알고리즘' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<br/>
<hr/>

### Binary Search

\<이분 탐색 Binary Search\>. 이분 탐색은 인류 지성의 가장 직관적이고 탁월한 도구다! 정말 개인적인 의견으론, 이 알고리즘이 내가 되고, 내가 이 알고리즘이 되는 \<몰아일체 物我一體\> 수준에 이르기 위해 정진해야 할 정도로 "인생"에서 중요한 알고리즘이라고 생각한다.

아이디어는 간단하다. "절반으로 줄이며 탐색하기". 나는 이걸 \<관심 영역 Interest Zone\>을 쳐낸다고 정의했다. 일종의 \<가지 치기 Pruning\>라고 생각한다는 말이다. 🌴

\<분할 정복\>과는 약간 스타일이 다르다고도 생각하는데, 분할 정복은 문제를 분할하고 이후에 베이스 케이스부터 다시 쌓아올려야 하지만, \<이분 탐색\>은 쌓아올리는 과정 없이 분할만 수행한다.

<hr/>

포스트의 목적이 수업 내용 정리니 일단 정리를 해보자!

<div class="img-wrapper">
  <img src="{{ "/images/algorithm/binary-search-1.jpg" | relative_url }}" width="320px">
</div>

**Goal**: Find a key $k$ in sorted order array.

먼저 target $k$를 배열의 가운뎃 값과 비교한다. 비교 결과에 따라 좌측 절반을 취하거나 우측 절반을 취한다. 이후 그 절반에 대해서 동일한 과정을 반복한다!

\<분할 정복\>의 관점에서 볼 때, 단 하나의 subproblem이 발생하기 때문에 $a=1$이다. 따라서

$$
T(n) = T(n/2) + O(1)
$$

\<Master Theorem\>을 적용하자. $a=1$, $b=2$, $c=0$이므로 $a/b^c = 1$이다. 따라서

$$
O(1) \cdot \log n = O(\log n)
$$

$\blacksquare$

<hr/>

뭔가 이대로 포스트를 끝내기엔 아쉬워서 PS에서 흔히 하는 실수 중 하나에 대해 말해보려고 한다.

#### Off-by-One

> "This problem could arise when a programmer makes mistakes such as using "is less than or equal to" where "is less than" should have been used in a comparison." - [Wikipedia](https://en.wikipedia.org/wiki/Off-by-one_error)

이분 탐색을 포함한, 대부분의 분할 정복 문제에서 "Off-be-One"은 정말 개발자를 화나게 하는 오류이자 실수다!! 흔히, 하나를 덜 포함하거나 더 포함해서 생기는 실수다 😱😱

분할 정복의 경우, 유독 ceil $\lceil x \rceil$을 취할지, floor $\lfloor x \rfloor$를 취할지 헷갈리는 경우가 많다. 또는, iteratoring 과정에서 `arr[0]`을 포함할지나 `arr[last+1]`을 포함해야 하는지 등등 정말 많은 부분에서 그 "**하나**" 때문에 특수한 케이스에서 FAIL을 받게 만든다.

본인이 생각하는 이 실수를 줄이는 방법은 결국, **\<자기 의심 self-doubting\>**이다. 분할 정복으로 접근할 때, `if`문의 조건을 제대로 쓴 건지, 자신을 의심하는 거다. 쉽게 말하면 대충 넘어가지 말고 꼼꼼히 봐라는 말이다.

<br/>

최근에 Off-by-One 때문에 시달린 문제가 있어서 링크를 걸어둔다.

- [[BAEKJOON] 1654번 - 랜선 자르기](https://www.acmicpc.net/problem/1654) 
