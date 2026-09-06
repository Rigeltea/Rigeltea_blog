---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-two-people-and-cards/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Bitonic Cycle

## 두 사람과 카드

Easy

30XP

평균 28분

67% 정답률

총 제출 74회

정수 값이 적혀있는 $n$ 개의 카드가 주어지고 두 사람이 협력하여 게임을 진행합니다. 왼쪽에서부터 카드를 보며 두 사람 중 한 사람이 그 카드를 가져갑니다.

이때 각 사람의 점수는 뽑은 수들을 순서대로 나열했을 때 인접한 수들간의 차이의 합이 됩니다. 카드를 적절하게 분배하여 두 사람의 점수의 합이 최소가 되도록 하는 프로그램을 작성해보세요.

예를 들어 {5, 2, 6, 1, 9} 순으로 주어졌을 때 첫 번째 사람이 순서대로 {5, 2, 9}, 두 번째 사람이 순서대로 {6, 1}을 뽑았다면 두 사람은 각각 |5 - 2| + |2 - 9| = 10, |6 - 1| = 5 점을 얻게 됩니다. 하지만 만약 첫 번째 사람이 {5, 6, 9}, 두 번째 사람이 {2, 1}를 뽑았다면 두 사람은 각각 |5 - 6| + |6 - 9| = 4, |2 - 1| = 1 점을 얻게되어 합이 5점으로 최소가 됩니다.

### 입력

첫 번째 줄에 $n$ 이 주어집니다.

두 번째 줄에는 $n$ 개의 카드 정보가 공백을 사이에 두고 주어집니다.

### 제한 조건

- $1 \le n \le 2,000$
- $1 \le$ 카드에 적혀있는 수 $\le 1,000,000$

### 출력

카드를 적절하게 분배했을 때 가능한 두 사람의 점수의 합 중 최솟값을 출력합니다.

### 입력 예제

### 예제 1

입력

```
5
5 2 6 1 9
```

출력

```
5
```

### 예제 2

입력

```
5
1 2 3 4 5
```

출력

```
3
```

### 제한

• Time Limit: 2000 ms

• Memory Limit: 192 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!