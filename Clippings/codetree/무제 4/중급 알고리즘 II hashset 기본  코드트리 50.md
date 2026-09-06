---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-longest-relay/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. Bitmask DP

## 최장 릴레이

Medium

60XP

평균 39분

43% 정답률

총 제출 62회

$n$ 명의 사람이 서있습니다. $1$ 번 사람을 시작으로 하여 최대한 많은 사람들이 릴레이를 이어가려고 합니다. 한 사람이 두 번 이상 릴레이에 참여할 수는 없으며, 릴레이에 참여한 순서가 $a_1, a_2, ..., a_k$ 라 했을 때 $0 < A[a_1][a_2] < A[a_2][a_3] < ... < A[a_{k-1}][a_k]$ 를 만족해야 한다고 합니다. 조건을 만족하는 경우 중 최대로 릴레이에 참여할 수 있는 사람 수를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $n$ 이 주어집니다.

두 번째 줄부터는 $n$ 개의 줄에 걸쳐 각 행에 해당하는 $A_{ij}$ 값이 공백을 사이에 두고 주어집니다.

### 제한 조건

### 출력

조건을 만족하는 경우 중 최대로 릴레이에 참여할 수 있는 사람 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
0 1 2
1 0 2
2 1 0
```

출력

```
3
```

### 예제 2

입력

```
4
0 2 2 1
1 0 4 3
3 3 0 3
0 0 0 0
```

출력

```
3
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!