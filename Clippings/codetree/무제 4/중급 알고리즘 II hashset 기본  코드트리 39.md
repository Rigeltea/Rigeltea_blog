---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-bitonic-cycle-2/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Bitonic Cycle

## Bitonic Cycle 2

Medium

60XP

평균 72분

26% 정답률

총 제출 106회

2차 평면상 위에 서로 다른 $N$ 개의 점이 주어집니다. $N$ 개의 점들의 $x$ 좌표 값들은 전부 다르게 주어집니다. 가장 작은 $x$ 좌표를 갖는 점에서 시작하여 가장 큰 $x$ 좌표를 갖는 곳까지는 $x$ 좌표가 증가하는 순으로 이동하고, 다시 시작 위치로 돌아올 때에는 $x$ 좌표가 감소하는 순으로 이동해야 한다고 합니다. 오고 가는 가운데 모든 점을 방문해야 하며, 가능한 최소 거리의 합을 구하는 프로그램을 작성해보세요. 단, 이 문제에서는 특별하게도 거리의 합 계산시 **정확히 한 번만 두 점 사이의 거리를 $0$ 으로 계산** 하는 것이 가능하다고 합니다. 또한 이 문제에서 두 점 $(x_1,\ y_1)$, $(x_2,\ y_2)$ 사이의 거리는 $(x_1 - x_2)^2 + (y_1 - y_2)^2$ 으로 정의됩니다.

### 입력

첫 번째 줄에 $N$ 이 주어집니다.

두 번째 줄부터는 $N$ 개의 줄에 걸쳐 각 점의 위치 $(x,\ y)$ 가 공백을 사이에 두고 한 줄에 하나씩 주어집니다.

### 제한 조건

### 출력

가장 작은 $x$ 좌표를 갖는 점에서 시작하여 규칙을 만족하며 모든 점을 방문하고 돌아오는 경우 중 가능한 최소 거리의 합을 출력합니다. 거리의 합 계산시 정확히 한 번에 한하여 두 점 사이의 거리를 $0$ 으로 계산하는 것이 가능함에 유의합니다.

### 입력 예제

### 예제 1

입력

```
4
3 3
2 4
1 2
4 5
```

출력

```
12
```

예제 설명

접기

예제 $1$ 번에서는 $3\to2\to1\to4\to3$ 순으로 방문했을 때 문제 조건을 만족하게 되며 $4\to3$ 에 해당하는 거리를 $0$ 으로 두면 거리의 합이 $5+2+5+0=12$ 로 최소가 됩니다.

### 예제 2

입력

```
5
3 3
2 4
1 2
4 5
5 9
```

출력

```
29
```

### 제한

• Time Limit: 7000 ms

• Memory Limit: 420 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!