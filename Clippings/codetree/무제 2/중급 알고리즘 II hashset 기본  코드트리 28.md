---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-the-sum-of-the-subsequences-is-k/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Prefix Sum

## 부분 수열의 합이 K

Easy

20XP

평균 18분

82% 정답률

총 제출 857회

$N$ 개의 정수로 이루어진 수열에서 연속된 구간의 합을 구하려합니다.

모든 연속된 구간의 합 중에서 합이 $K$ 인 것의 개수를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 정수 $N$ 과 $K$ 가 공백을 두고 주어집니다.

두 번째 줄에 $N$ 개의 정수가 공백을 두고 주어집니다.

### 제한 조건

- $3 \le N \le 1\,000$
- $1 \le K \le 1\,000\,000$
- $1 \le \texttt{주어진 정수의 값} \le 1\,000\,000$

### 출력

첫 번째 줄에 모든 연속된 구간의 합 중에서 합이 $K$ 인 것의 개수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
4 3
1 2 1 2
```

출력

```
3
```

예제 설명

접기

합이 $3$ 이 되는 $3$ 개의 구간은 다음과 같습니다.

\[$1$, $2$\], \[$2$, $1$\], \[$1$, $2$\]

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!