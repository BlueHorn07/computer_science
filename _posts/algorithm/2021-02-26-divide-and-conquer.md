---
title: "Divide and Conquer"
layout: post
use_math: true
tags: ["Algorithm"]
---

### 서론
2020-1학기, 대학에서 '알고리즘' 수업을 듣고 공부한 바를 정리한 글입니다. 지적은 언제나 환영입니다 :)

<br/>
<hr/>

### Divide and Conquer

\<분할 정복 Divide and Conquer\>는 문제를 해결하는 접근법 중 하나다. 그 과정을 간략히 기술하면 아래와 같다.

1. Break the problem into "subproblems".
2. Solve them recursively.
3. Combine the solutions to get the answer to the problem.

**분할 정복**은 기본적으로 \<재귀 Recursion\>을 기반으로 한다. 문제를 \<하위 문제 subproblem\>로 분할하고, 그 하위 문제를 더 하위의 문제로 분할한다. 분할은 손쉽게 다룰 수 있는 수준인 베이스 케이스 진행된다. 이후엔 분할한 규칙에 따라 하위 문제에서 얻은 결과를 상위 문제에서 차례대로 조합(Combine) 해주면 원래 문제에 대한 정답을 얻는다.

<div class="img-wrapper">
  <img src="{{ "/assets/img/algorithm/divide-and-conquery-1.jpg" | relative_url }}" width="500px">
</div>

<hr/>

1. [Multiplication Algorithm]({{"2021/02/26/multiplication-algorithm.html" | relative_url}})
2. Binary Search
3. Merge Sort
4. Matrix Mutliplication - Volker Strassen Method
5. Find Medians and Selection
6. Closest pair of points
