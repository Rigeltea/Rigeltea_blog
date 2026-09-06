---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-the-sum-of-the-numbers-is-a-multiple-of-7/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. 전처리

## 숫자들의 합이 7의 배수

Medium

60XP

평균 57분

47% 정답률

총 제출 604회

$N$ 개의 서로 다른 수가 차례대로 주어집니다. 이들 중 연속하게 고른 수들의 합이 $7$ 의 배수가 되게 그룹으로 묶으려 합니다. 이렇게 만든 그룹 중 최대 크기를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$ 이 주어집니다.

두 번째 줄부터 $N$ 개의 줄에 걸쳐 수가 각 줄에 한 개씩 차례대로 주어집니다.

### 제한 조건

- $1 \le N \le 50\,000$
- $0 \le \texttt{주어지는 수} \le 1\,000\,000$

### 출력

첫 번째 줄에 조건을 만족하는 그룹 중 최대 크기를 출력합니다. 만약 불가능하다면 $0$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
7
3
5
1
6
2
14
10
```

출력

```
5
```

예제 설명

접기

$5$, $1$, $6$, $2$, $14$ 를 그룹으로 묶으면 $5 + 1 + 6 + 2 + 14 = 28$ 이 되어 $7$ 의 배수가 됩니다. 이보다 큰 그룹을 만들 수 있는 방법은 없습니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!