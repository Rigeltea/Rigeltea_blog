---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-two-adjacent-numbers-and-sum/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 작은 구간에서 큰 구간으로 확장되는 DP

## 인접한 두 수와 합

Medium

60XP

평균 49분

71% 정답률

총 제출 38회

$N$ 개의 수가 왼쪽부터 순서대로 주어졌을 때, 하나의 수가 남을 때까지 인접한 두 수를 골라 없애는 것을 반복하려고 합니다. 인접한 두 수를 고르게 되면 두 수의 차만큼의 점수를 얻게 되고 두 수가 사라짐과 동시에 해당 위치에 두 수의 합만큼에 해당하는 새로운 수가 추가된다고 합니다. 이러한 조건 하에서 얻을 수 있는 최대 점수를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$ 이 주어집니다.

두 번째 줄에는 $N$ 개의 수가 공백을 사이에 두고 주어집니다.

### 제한 조건

- $1 \le N \le 500$
- $1 \le \texttt{주어지는 수} \le 10\,000$

### 출력

하나의 수가 남기 전까지 얻을 수 있는 최대 점수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
4
6 5 8 2
```

출력

```
27
```

예제 설명

접기

예제 1번에서는 다음 전략을 통해 $27$ 점을 얻을 수 있습니다.

- 처음 $(5,\ 8)$ 을 골라 점수 $3$ 을 얻고 수 $13$ 을 새로 적어줍니다. 즉, $6\ 13\ 2$ 가 남게 됩니다.
- $(6,\ 13)$ 을 골라 점수 $7$ 을 얻고 수 $19$ 를 새로 적어줍니다. 즉, $19\ 2$ 가 됩니다.
- $(19,\ 2)$ 를 골라 점수 $17$ 을 얻고 수 $21$ 을 새로 적어줍니다.

따라서 $3+7+17=27$ 점을 얻게 됩니다.

### 예제 2

입력

```
4
6 5 8 20
```

출력

```
62
```

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!