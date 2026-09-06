---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-symmetric-difference-set/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. HashSet

## 대칭 차집합

Easy

20XP

평균 9분

77% 정답률

총 제출 1,130회

대칭 차집합이란?

- 대칭 차집합이란, 두 집합 $A$ 와 $B$ 가 있을 때 집합 $A - B$ 와 집합 $B - A$ 의 합집합을 대칭 차집합 이라고 한다.

자연수를 원소로 갖는 두 집합 $A$ 와 $B$ 에 대한 대칭 차집합의 원소의 개수를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에는 집합 $A$ 의 원소의 개수와 집합 $B$ 의 원소의 개수가 공백을 두고 주어집니다.

두 번째 줄에는 집합 $A$ 의 모든 원소가 공백을 두고 주어집니다.

세 번째 줄에는 집합 $B$ 의 모든 원소가 공백을 두고 주어집니다.

### 제한 조건

- $1 \le \texttt{집합의 원소의 개수} \le 200\,000$
- $0 \le \texttt{원소의 값} \le 10^9$
- 모든 원소는 정수이며, $A$, $B$ 각각의 집합 안에서는 같은 원소가 여러 번 주어지지 않습니다.

### 출력

첫 번째 줄에 대칭 차집합의 원소의 개수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
3 3
1 2 6
2 6 9
```

출력

```
2
```

예제 설명

접기

예제 $1$ 번에서, 집합 $A - B$ 는 $(1)$ 이고, 집합 $B - A$ 는 $(9)$ 이므로, 대칭 차집합은 $(1,\ 9)$ 입니다. 따라서 원소의 개수는 $2$ 개입니다.

### 예제 2

입력

```
5 6
1 4 7 9 22
3 7 22 35 134 1235
```

출력

```
7
```

예제 설명

접기

예제 $2$ 번에서, 집합 $A - B$ 는 $(1,\ 4,\ 9)$ 이고, 집합 $B - A$ 는 $(3,\ 35,\ 134,\ 1235)$ 이므로, 대칭 차집합은 $(1,\ 3,\ 4,\ 9,\ 35,\ 134,\ 1235)$ 입니다. 따라서 원소의 개수는 $7$ 개입니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 160 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!