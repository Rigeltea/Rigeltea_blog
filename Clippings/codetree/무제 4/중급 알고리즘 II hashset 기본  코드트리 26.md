---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-possible-path-of-travel/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Graph DP

## 갈 수 있는 경우의 수

Easy

30XP

평균 46분

70% 정답률

총 제출 168회

$n$ 개의 노드와 $m$ 개의 간선으로 이루어진 단방향 그래프가 주어졌을 때, $1$ 번 노드에서 출발하여 $n$ 번 노드로 이동 가능한 서로 다른 경로의 수를 구하는 프로그램을 작성해보세요. 단, 주어지는 그래프에서는 사이클이 존재하지 않음을 가정해도 좋습니다.

### 입력

첫 번째 줄에 $n$ 과 $m$ 이 공백을 사이에 두고 주어집니다.

두 번째 줄 부터는 $m$ 개의 줄에 걸쳐 간선의 정보 $(x, y)$ 가 공백을 사이에 두고 주어집니다. 이는 $x$ 에서 $y$ 로 가는 간선이 존재함을 의미합니다.

### 제한 조건

- $1 \le n, m \le 100\,000$
- $1 \le x, y \le n, x \neq y$

### 출력

첫 번째 줄에 가능한 서로 다른 경우의 수 10억 7로 나눈 나머지를 출력합니다.

### 입력 예제

### 예제 1

입력

```
4 4
2 3
3 4
1 2
1 4
```

출력

```
2
```

### 예제 2

입력

```
4 3
2 4
3 2
1 3
```

출력

```
1
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!