---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-belonging-to-a-rock/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Prefix Sum

## 돌의 소속

Easy

40XP

평균 27분

81% 정답률

총 제출 603회

$1$ 부터 $N$ 까지 번호가 붙은 $N$ 개의 돌이 있습니다. 각 돌은 그룹 $1$, $2$, $3$ 중 하나에 무조건 속합니다. 각 돌이 어떤 그룹에 속하는지 주어졌을 때, $Q$ 개의 돌 번호 범위마다 각 그룹의 돌이 몇개씩 있는지 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$, $Q$ 가 주어집니다. $Q$ 는 주어진 범위의 개수입니다.

두 번째 줄부터 $N$ 개의 줄에 걸쳐 $i + 1$ 번째 줄에 $i$ 번 돌이 속한 그룹이 주어집니다.

$N + 2$ 번째 줄부터 $Q$ 개의 줄에 걸쳐 $N + i + 1$ 번째 줄에 $i$ 번째 범위에 대한 정보가 주어집니다. 각 범위는 $a, b$ 로 주어지며 이는 $a$ 이상 $b$ 이하를 의미합니다.

### 제한 조건

### 출력

첫 번째 줄부터 $Q$ 개의 줄에 걸쳐 $i$ 번째 줄에 $i$ 번째 범위 내에 있는 $1$, $2$, $3$ 번 그룹의 돌 개수를 공백을 사이에 두고 출력합니다.

### 입력 예제

### 예제 1

입력

```
6 3
2
1
1
3
2
1
1 6
3 3
2 4
```

출력

```
3 2 1
1 0 0
2 0 1
```

예제 설명

접기

$1$ 번과 $6$ 번 사이에는 $1$, $2$, $3$ 그룹의 돌이 각각 $3$, $2$, $1$ 개씩 있습니다.

$3$ 번과 $3$ 번 사이에는 $1$, $2$, $3$, 그룹의 돌이 각각 $1$, $0$, $0$ 개씩 있습니다.

$2$ 번과 $4$ 번 사이에는 $1$, $2$, $3$ 그룹의 돌이 각각 $2$, $0$, $1$ 개씩 있습니다.

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!