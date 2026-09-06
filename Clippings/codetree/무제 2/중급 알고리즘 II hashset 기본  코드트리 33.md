---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-count-number-of-points/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Grid Compression

## 점 개수 세기

Medium

80XP

평균 44분

44% 정답률

총 제출 791회

수직선 상의 서로 다른 위치에 $N$ 개의 점이 주어졌을 때, $Q$ 개의 질의에 대해 각각 구간 내 점의 개수를 출력하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ 과 $Q$ 가 공백을 사이에 두고주어집니다.

두 번째 줄에는 수직선 상에서 점 $N$ 개의 위치가 공백을 사이에 두고 주어집니다.

세 번째 줄 부터는 $Q$ 개의 줄에 걸쳐 구간에 대한 정보 $a_i$, $b_i$ 값이 공백을 사이에 두고 주어집니다. 이는 $a_i \le x \le b_i$ 를 만족하는 위치에 있는 점의 개수를 세어야 함을 의미합니다. 단, 중복되는 점은 주어지지 않습니다.

### 제한 조건

- $1 \le N, Q \le 100\,000$
- $-10^9 \le \texttt{주어지는 점의 위치} \le 10^9$
- $-10^9 \le a_i \le b_i \le 10^9$

### 출력

$Q$ 개의 질의에 대해 각 구간 내에 놓여있는 점의 개수를 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
3 2
-3 5 9
-3 4
-10 10
```

출력

```
1
3
```

예제 설명

접기

$(-3, 4)$ 구간 안에는 점 $-3$ 이 존재합니다.

$(-10, 10)$ 구간 안에는 점 $-3, 5, 9$ 가 존재합니다.

![](https://contents.codetree.ai/problems/2208/images/problems-b18efe2d-f0d2-42de-a7eb-3786ed74159e.png)

### 제한

• Time Limit: 4000 ms

• Memory Limit: 128 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!