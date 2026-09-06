---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-subsequence-with-k-or-more-1s/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Two Pointer

## 1이 K개 이상 존재하는 부분 수열

Easy

30XP

평균 27분

50% 정답률

총 제출 730회

$1$ 과 $2$ 로만 이루어진 길이 $N$ 의 수열에서, $1$ 이 $K$ 개 이상 존재하는 가장 짧은 연속된 부분 수열의 길이를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 두 정수 $N$ 과 $K$ 가 주어집니다.

두 번째 줄에 $N$ 개의 수가 주어집니다.

### 제한 조건

- $1 \le K \le N \le 1\,000\,000$
- 주어지는 수는 $1$ 또는 $2$ 입니다.

### 출력

$1$ 이 $K$ 개 이상 존재하는 연속된 부분 수열 중 가장 짧은 부분 수열의 길이를 출력합니다.

만약 그러한 부분 수열이 없다면, $-1$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
8 2
1 2 2 2 1 2 1 2
```

출력

```
3
```

예제 설명

접기

$5$, $6$, $7$ 번째 원소로 이루어진 부분 수열 \[$1$, $2$, $1$\] 은 $1$ 을 두 개 이상 포함하면서, 길이가 $3$ 으로 가장 짧습니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 240 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!