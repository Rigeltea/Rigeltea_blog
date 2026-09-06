---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-determining-the-suitability-of-the-route-2/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Disjoint Set (Union Find)

## 경로의 적합성 판단 2

Easy

30XP

평균 35분

55% 정답률

총 제출 484회

$n$ 개의 정점과 $m$ 개의 간선으로 이루어진 양방향 그래프가 있습니다.

$k$ 개의 점으로 이루어진 순서가 주어졌을 때, 그래프 위에서 주어진 순서대로 이동하는 것이 가능한지를 판단하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 정점의 개수 $n$, 간선의 수 $m$, 그리고 순서의 길이 $k$ 가 공백을 사이에 두고 주어집니다.

두 번째 줄부터 $m$ 개의 줄에 걸쳐 간선에 대한 정보 $(x, y)$ 가 공백을 사이에 두고 주어집니다. 이는 두 정점 $x, y$ 가 간선을 통해 연결되어 있음을 뜻하며, 동일한 간선이 여러번 주어지는 경우는 없다고 가정해도 좋습니다.

마지막 줄에는 $k$ 개의 점으로 이루어진 순서 정보가 공백을 사이에 두고 순서대로 주어집니다.

### 제한 조건

- $1 \leq n, m \leq 100,000$
- $1 \leq k \leq 100,000$
- $1 \leq x, y \leq n, x \neq y$

### 출력

주어진 순서대로 이동하는 것이 가능하다면 $1$ 을, 불가능하다면 $0$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
4 3 2
3 1
3 4
4 2
1 2
```

출력

```
1
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 100 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!