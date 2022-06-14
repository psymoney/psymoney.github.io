---
title: '[Solved]BOJ: 12865'
categories: PS
tags: BOJ solved
author_profile: true
published: true
---
## [12865. 평범한 배낭](https://www.acmicpc.net/problem/12865)

### 풀이
```python
def knapsack(N, K, W, V):
    m = [[0] * (K + 1) for _ in range(N + 1)]
    for n in range(N):
        for k in range(1, K + 1):
            a = 0
            b = m[n-1][k]
            c = 0
            if k >= W[n]:
                a = V[n]
                c = m[n-1][k-W[n]] + V[n]
            m[n][k] = max(a, b, c)
    return m[N - 1][K]


N, K = input().split()
N,K = int(N), int(K)
W = [None] * N
V = [None] * N

for i in range(N):
    w, v = input().split()
    W[i] = int(w)
    V[i] = int(v)
    
print(knapsack(N, K, W, V))
```
