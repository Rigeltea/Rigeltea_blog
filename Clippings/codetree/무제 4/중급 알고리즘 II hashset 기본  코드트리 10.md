---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-count-colored-node/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. LCA

## 트리 위에 색칠된 정점 수

Medium

60XP

평균 45분

61% 정답률

총 제출 83회

$n$ 개의 정점으로 이루어진 트리가 주어집니다. 이 트리의 루트는 $1$ 입니다.

$k$ 개의 색칠된 정점 번호가 주어집니다.

특정 노드부터 특정 노드까지 가는 경로는 단 한가지 뿐입니다. $q$ 개의 쿼리에 대해 특정 노드부터 특정 노드까지 가는 경로 상에 존재하는 서로 다른 색칠된 노드의 개수를 출력하는 프로그램을 작성해보세요.

이때, 경로의 시작과 끝 또한 포함됩니다.

### 입력

첫 번째 줄에 노드의 개수 $n$ 이 주어집니다.

두 번째 줄부터 $n$ 번째 줄까지 총 $n-1$ 개의 줄에 걸쳐 간선으로 연결된 두 개의 노드가 공백을 두고 차례대로 주어집니다.

$n+1$ 번째 줄에는 색칠된 정점 수 $k$ 가 주어집니다.

$n+2$ 번째 줄부터 $k$ 줄에 걸쳐 색칠된 정점의 번호가 차례로 주어집니다.

$n+k+2$ 번째 줄에는 쿼리의 개수 $q$ 가 주어집니다.

$n+k+3$ 번째 줄부터 $q$ 개의 줄에 경로의 시작과 끝을 의미하는 두 정점의 쌍이 공백을 두고 차례대로 주어집니다.

### 제한 조건

- $$
	1 \le k \le n \le 100\,000
	$$
- $$
	1 \le q \le 100\,000
	$$
- $1 \le$ 노드의 번호 $\le n$

### 출력

쿼리에서 차례대로 각 줄마다 입력받은 두 정점을 시작과 끝으로 하는 경로사이에 서로 다른 색칠된 노드의 개수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
15
1 2
1 3
2 4
3 7
6 2
3 8
4 9
2 5
5 11
7 13
10 4
11 15
12 5
14 7
4
2
6
7
11
6
6 11
10 9
2 6
7 6
8 13
8 15
```

출력

```
3
0
2
3
1
2
```

### 제한

• Time Limit: 4000 ms

• Memory Limit: 320 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!