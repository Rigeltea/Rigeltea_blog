---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-sum-of-consecutive-n-integers/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Two Pointer

## 연속하는 정수 N개의 합

Easy

30XP

평균 20분

73% 정답률

총 제출 877회

크기가 $N$ 인 수열이 주어졌을 때, 이 중 연속하는 몇 개의 원소들의 합이 $M$ 이 되는 경우의 수를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 수열의 크기와 구하려는 원소들의 합을 나타내는 두 정수 $N$ 과 $M$ 이 주어집니다.

두 번째 줄에 $N$ 개의 정수가 공백으로 구분되어 차례대로 주어집니다.

### 제한 조건

- $1 \le N \le 100\,000$
- $1 \le M \le 300\,000\,000$
- $1 \le \texttt{수열의 원소} \le 30\,000$

### 출력

첫 번째 줄에 원소들의 합이 $M$ 이 되는 경우의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
5 7
1 3 2 4 1
```

출력

```
1
```

예제 설명

접기

연속하는 몇 개의 원소의 합이 $7$ 인 경우는 $2,\  4,\  1$ 뿐입니다.

### 예제 2

입력

```
4 2
1 1 1 1
```

출력

```
3
```

예제 설명

접기

연속하는 몇 개의 원소의 합이 $2$ 인 경우는 `1 번째 원소와 2 번째 원소`, `2 번째 원소와 3 번째 원소`, `3 번째 원소와 4 번째 원소` 로 $3$ 가지 입니다.

### 예제 3

입력

```
10 5
1 2 3 4 2 5 3 1 1 2
```

출력

```
3
```

예제 설명

접기

연속하는 몇 개의 원소의 합이 $5$ 인 경우는 \[$2$, $3$\], \[$5$\], \[$3$, $1$, $1$\] 로 $3$ 개입니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!