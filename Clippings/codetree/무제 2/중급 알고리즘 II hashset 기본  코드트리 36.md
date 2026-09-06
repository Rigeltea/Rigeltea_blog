---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-divide-by-equal-sum-of-intervals/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. LR Technique

## 구간의 합이 같게 나누기

Hard

90XP

평균 180분

53% 정답률

총 제출 493회

$N$ 개의 정수로 이루어진 수열을 $4$ 개의 구간으로 나누려합니다.

각 구간은 최소한 한 개의 원소를 포함해야 하며, 각 구간에서 원소의 합은 같아야합니다.

몇 가지의 방법으로 주어진 수열을 $4$ 개의 구간으로 나눌 수 있는지 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$ 이 주어집니다.

두 번째 줄에 $N$ 개의 정수가 공백을 두고 주어집니다.

### 제한 조건

- $4 \le N \le 100\,000$
- $-2 \times 10^9 \le \texttt{주어지는 정수} \le 2 \times 10^9$

### 출력

수열을 문제의 조건을 만족하며 $4$ 개의 구간으로 나눌 수 있는 경우의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
10
4 -1 2 1 -3 1 2 2 1 3
```

출력

```
3
```

예제 설명

접기

수열 \[$4$, $-1$, $2$, $1$, $-3$, $1$, $2$, $2$, $1$, $3$\] 을 원소의 합이 같은 $4$ 개의 구간으로 나누는 경우는 다음 $3$ 가지 입니다.

1. \[$4$, $-1$\], \[$2$, $1$, $-3$, $1$, $2$\], \[$2$, $1$\], \[$3$\]
2. \[$4$, $-1$\], \[$2$, $1$\], \[$-3$, $1$, $2$, $2$, $1$\], \[$3$\]
3. \[$4$, $-1$, $2$, $1$, $-3$\], \[$1$, $2$\], \[$2$, $1$\], \[$3$\]

### 예제 2

입력

```
5
0 0 0 0 0
```

출력

```
4
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!