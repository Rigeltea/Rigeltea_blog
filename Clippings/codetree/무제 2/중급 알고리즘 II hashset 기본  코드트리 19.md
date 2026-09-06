---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-top-3-smallest-number/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. Priority Queue

## 최솟값 3개

Easy

20XP

평균 15분

47% 정답률

총 제출 1,326회

$N$ 개의 숫자가 순서대로 하나씩 주어졌을 때, 숫자가 하나씩 주어질 때마다 지금까지 주어진 숫자들 중 가장 작은 숫자 $3$ 개의 곱을 출력하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ 이 주어집니다.

두 번째 줄에는 $N$ 개의 숫자가 공백을 사이에 두고 주어집니다.

### 제한 조건

- $1 \le N \le 100\,000$
- $1 \le \texttt{주어지는 숫자들} \le 100\,000$

### 출력

$N$ 개의 숫자가 순서대로 하나씩 주어질 때마다 지금까지 주어진 숫자들 중 가장 작은 숫자 $3$ 개의 곱을 한 줄에 하나씩 출력합니다. 만약 아직 주어진 숫자의 수가 채 $3$ 개가 되지 않는다면, $-1$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
5
1 5 2 7 3
```

출력

```
-1
-1
10
10
6
```

예제 설명

접기

첫 번째 숫자 $1$ 과 두 번째 숫자 $5$ 가 주어졌을 때 까지는 아직 주어진 숫자가 $3$ 개가 채 되지 않으므로 $-1$ 이 답이 됩니다.

세 번째 숫자 $2$ 가 주어진 이후에는 최솟값 $3$ 개가 \[$1$, $2$, $5$\]가 되므로 답은 $10$ 이 됩니다.

네 번째 숫자 $7$ 이 주어진 이후에도 최솟값 $3$ 개가 \[$1$, $2$, $5$\]가 되므로 답은 $10$ 이 됩니다.

다섯 번째 숫자 $3$ 이 주어진 이후에는 최솟값 $3$ 개가 \[$1$, $2$, $3$\]이 되므로 답은 $6$ 이 됩니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!