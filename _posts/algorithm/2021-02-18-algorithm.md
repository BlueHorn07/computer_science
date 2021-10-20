---
title: "Algorithm"
layout: post
use_math: true
tags: ["Algorithm"]
hidden: true
---

<br>

🔥 2020-1학기 POSTECH 안희갑 교수님의 『Algorithm(CSED331)』을 수강하면서 공부한 내용을 정리하였습니다. 😁

#### 참고 교재
- 『Algorithms』 Dasgupta, international ed.
- [『알고리즘 문제해결전략』](https://book.algospot.com/) 구종만

<div class="math-statement" markdown="1">

[목차]

- Computational Complexity
- Divide and Conquery
- Graph Algorithm
- Greedy Algorithm
- Dynamic Programming
- Network Flow
- Linear Programming
- NP & NP-complete
- Appendix

</div>

<br/>
<hr/>

정규수업에서 다루지 않은 내용은 🎈로 표시하였습니다 😉

### Computational Complexity

- [Asymptotic Analysis]({{"/2021/05/14/asymptotic-analysis.html" | relative_url}})
  - Big-O / Big-Omega / Big-Theta
  - little-o / little-omega / little-theta
- [Master Theorem: Recurrence relations]({{"/2021/02/26/divide-and-conquer.html#master-theorem-recurrence-relations" | relative_url}})
- [Fibonacci Number]({{"/2021/05/15/fibonacci-number.html" | relative_url}})
  - Brute Force
  - DP
  - Matrix-based
- [Convex Hull Algorithm]({{"/2021/05/15/convex-hull-algorithm.html" | relative_url}})
  - Brute Force
  - Graham's Scan

### [Divide and Conquer]({{"2021/02/26/divide-and-conquer.html" | relative_url}})

- [Multiplication Algorithm]({{"2021/02/26/multiplication-algorithm.html" | relative_url}})
- [Binary Search]({{"2021/02/27/binary-search.html" | relative_url}})
  - Off-by-One
  - Approximate Matches
- [Merge Sort]({{"/2021/02/27/merge-sort.html" | relative_url}})
  - [Skyline Problem]({{"/2021/09/25/skyline-problem.html" | relative_url}}) 🎈
- [Matrix Multiplication: Strassen Algorithm]({{"/2021/10/19/matrix-multiplication-strassen-algorithm.html" | relative_url}})
- [Quick Selection]({{"/2021/10/21/quick-selection.html" | relative_url}})
- Closest pair of points

### Graph Algorithm

- [DFS and BFS]({{"/2021/03/12/dfs-and-bfs.html" | relative_url}})
  - [DFS and BFS - code]({{"/2021/03/13/dfs-and-bfs-code.html" | relative_url}})
- [DFS Tree]({{"/2021/03/13/dfs-tree.html" | relative_url}})
- [Dijkstra's Algorithm]({{"/2021/04/17/dijkstra-algorithm.html" | relative_url}})
- [Bellman-Ford Algorithm]({{"/2021/04/18/Bellman-Ford.html" | relative_url}})
- [DAG & Topological Sort]({{"/2021/04/19/directed-acyclic-graph.html" | relative_url}})

### [Greedy Algorithm]({{"/2021/04/19/greedy-algorithm.html" | relative_url}})

- MST; Minimum Spanning Tree
  - [Kruskal's Algorithm]({{"/2021/04/19/kruskal-and-prim-algorithm.html#kruskals-algorithm" | relative_url}})
  - [Prim's Algorithm]({{"2021/04/19/kruskal-and-prim-algorithm.html#prims-algorithm" | relative_url}})
  - Disjoint Set
    - Path Compression
- [Intervel Scheduling & Partitioning]({{"/2021/04/20/interval-scheduling-and-partitioning.html" | relative_url}})
- [Huffman Encoding]({{"/2021/10/08/Huffman-encoding.html" | relative_url}})
- Clustering of Maximum Spacing

### [Dynamic Programming]({{"/2021/04/20/dynamic-programming.html" | relative_url}})

- [LIS; Longest Incresaing Subsequences]({{"/2021/04/20/longest-increasing-subsequences.html" | relative_url}})
- [Edit Distance]({{"/2021/04/20/edit-distanace.html" | relative_url}})
  - [Dameraus-Levenshtein Distance]({{"/2021/04/24/Damerau-Levenshtein-distance.html" | relative_url}}) 🎈
- [Knapsack]({{"/2021/04/30/kanpsack.html" | relative_url}})
- [Chain Matrix Multiplication]({{"/2021/05/02/chain-matrix-multiplication.html" | relative_url}})
- [Shortest Reliable Paths]({{"/2021/06/13/shortest-reliable-paths.html" | relative_url}})
- [All Pairs Shortest Paths; Floyd-Warshall]({{"/2021/06/13/all-pairs-shortest-paths.html" | relative_url}})
- [TSP; Traveling Salesman Problem]({{"/2021/06/13/traveling-salesman-problem.html" | relative_url}})
  - 완전탐색
  - DP
- [Independent Sets in Tree]({{"/2021/07/10/independent-sets-in-tress.html" | relative_url}})
- [Weighted Interval Scheduling]({{"/2021/07/12/weighted-interval-scheduling.html" | relative_url}})
- [Segmented Least Squares]({{"/2021/07/12/segmented-least-squares.html" | relative_url}})

### Linear Programming

- Simplex Method

### [Network Flow]({{"/2021/07/16/network-flow.html" | relative_url}})

- [Max-Flow Min-Cut Theorem]({{"/2021/07/16/network-flow.html#residual-network" | relative_url}})
- [Ford-Fulkerson Algorithm & Edmons-Karp Algorithm]({{"/2021/10/03/ford-fulkerson-algorithm-and-edmons-karp-algorithm.html" | relative_url}})
- [Bipartite Matching]({{"/2021/10/04/bipartite-matching.html" | relative_url}})
- Variations of Network Flow Problem
- Dinic Algorithm 🎈

### NP & NP-complete

- Rudrata-Hamilton Cylcle Problem
- Balanced Cut
- 3D Matching
- Independent Set & Vertex Cover & Clique
- Longest Path Problem
- Subset Sum Problem

### Appendix

- [Amortized Analysis]({{"/2021/05/08/amortized-analysis.html" | relative_url}}) 🎈
  - Accounting Method
- [Implementations of Heap]({{"/2021/05/03/implementations-of-heap.html" | relative_url}}) 🎈
  - Heap by unordered array & ordered array
  - Binary Heap
  - [d-ary Heap]({{"/2021/05/03/implementations-of-heap.html#d-ary-heap" | relative_url}})
  - [Binomial Heap]({{"/2021/05/03/implementations-of-heap.html#binomial-heap" | relative_url}})
    - Binomial Tree
  - [Lazy-Binomial Heap]({{"2021/05/03/implementations-of-heap.html#lazy-binomial-heap" | relative_url}})
  - [Fibonacci Heap]({{"/2021/05/03/implementations-of-heap.html#fibonacci-heap" | relative_url}}) 🔥
- FFT; Fast Fourier Transformation 🎈

<hr/>

