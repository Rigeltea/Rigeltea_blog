---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-dot-to-the-dot/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

## 닷 투더 닷

Hard

90XP

평균 180분

60% 정답률

총 제출 194회

$1$ 부터 $N$ 까지 번호가 붙은 서로 다른 $N$ 개의 점과 이 점들 중 임의의 두 점을 잇는 선분 $M$ 개가 있습니다. 두 점을 잇는 선분은 여러 개가 될 수 있으며, 각 선분을 통해 점들 사이를 이동할 수 있습니다. 각 선분은 고유한 $L$ 값과 $C$ 값을 가집니다. 우리는 $1$ 번 점부터 $N$ 번 점까지 이동하려 합니다. 이때 사용된 모든 선분들의 $C$ 값 중 최솟값을 $A$, 모든 선분들의 $L$ 값의 합을 $B$, 주어진 임의의 값을 $X$ 라고 하면, 이 경로로 이동하는데 필요한 총 시간은 $B+X\div A$ 입니다. $1$ 번 점부터 $N$ 번 점까지 이동하는데 필요한 최소 시간을 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$, $M$, $X$ 가 공백을 사이에 두고 차례대로 주어집니다.

두 번째 줄부터 $M$ 개의 줄에 걸쳐, 각 줄에 각 선분의 양 끝점 번호 $I$, $J$ 와 $L$, $C$ 값이 공백을 사이에 두고 차례대로 주어집니다.

### 제한 조건

### 출력

첫 번째 줄에 $1$ 번 점부터 $N$ 번 점까지 이동하는데 필요한 최소 시간을 소수점을 버림하여 정수 형태로 출력하세요. $1$ 번 정점에서 $N$ 번 정점까지 이동 가능함이 보장됩니다.

### 입력 예제

### 예제 1

입력

```
3 3 15
1 2 10 3
3 2 10 2
1 3 14 1
```

출력

```
27
```

예제 설명

접기

경로 1 → 3은 $14 + 15 \div 1 = 29$ 단위 시간이 걸립니다. 경로 1 → 2 → 3은 $20 + 15 \div 2 = 27.5$ 단위 시간이 걸립니다. 따라서 필요한 최소 단위 시간은 $27.5$ 입니다.

![](https://contents.codetree.ai/problems/2058/images/problems-1fbd86fb-c76c-4c65-a660-ae0fb3020b7e.png)

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!