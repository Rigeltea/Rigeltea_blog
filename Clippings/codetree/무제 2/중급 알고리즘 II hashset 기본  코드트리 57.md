---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-use-the-swimming-pool-efficiently/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Parametric Search

## 수영장 효율적으로 활용하기

Easy

40XP

평균 50분

50% 정답률

총 제출 353회

$M$ 개의 레인이 있는 수영장이 있습니다. 수영장을 효율적으로 이용하기 위하여 다음 조건에 맞춰 각 사람마다 사용할 레인을 정해주려고 합니다.

- 총 $N$ 명의 사람이 수영장을 이용하게 되며, 수영장에 도착한 순서대로 $1$ 부터 $N$ 까지 번호를 매깁니다.
- $1$ 번부터 $N$ 번까지의 사람에 대해, $i$ 번째 사람의 수영장 이용시간은 $T_i$ 입니다.
- 레인별로 사람들을 할당합니다. 각 레인에는 $1$ 부터 $M$ 까지 번호가 매겨져 있고, 모든 사람들은 하나의 레인에만 할당되어야 하며, 도착한 순서가 늦은 사람이 할당받은 레인 번호가 먼저 도착한 사람의 레인 번호보다 앞설 수 없습니다.

위의 조건을 만족시키며, 레인별 사람들의 수영장 이용시간의 합들 중 최댓값을 최소화하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ 과 $M$ 이 주어집니다.

두 번째 줄에는 사람별 수영장 이용시간이 공백을 사이에 두고 주어집니다.

### 제한 조건

### 출력

첫 번째 줄에 가능한 각 레인 별 수영장 이용시간의 총합 중 최댓값의 최솟값을 출력합니다.

### 입력 예제

### 예제 1

입력

```
8 4
13 2 3 8 11 5 3 12
```

출력

```
16
```

예제 설명

접기

$1$ 번 레인에 $1$ 번 사람을 넣으면 수영 이용시간 총합은 $13$ 입니다.

$2$ 번 레인에 $2$, $3$, $4$ 번 사람을 넣으면 수영 이용시간 총합은 $13\,(2+3+8)$ 입니다.

$3$ 번 레인에 $5$, $6$ 번 사람을 넣으면 수영 이용시간 총합은 $16\,(11+5)$ 입니다.

$4$ 번 레인에 $7$, $8$ 번 사람을 넣으면 수영 이용시간 총합은 $15\,(3+12)$ 입니다.

따라서 이용시간 합 중 최댓값은 $16$ 이므로, 답은 $16$ 입니다.

이보다 이용시간 합 중 최댓값을 더 작게 만들 수는 없습니다.

![](https://contents.codetree.ai/problems/2222/images/problems-c8719411-4a72-425a-951e-73a01e732c1e.png)

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!