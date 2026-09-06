---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-max-num-outside-of-interval/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. LR Technique

## 구간 외 최대 숫자

Easy

40XP

평균 18분

83% 정답률

총 제출 281회

$N$ 개의 숫자가 주어졌을 때, $Q$ 개의 질의에 대해 주어진 구간 밖에 있는 숫자들 중 최댓값을 출력하는 프로그램을 작성해보세요.

단, 구간은 $N$ 개의 숫자의 번호에 해당하는 숫자로 주어집니다.

### 입력

첫 번째 줄에 $N$ 과 $Q$ 가 공백으로 구분되어 주어집니다.

두 번째 줄에는 $N$ 개의 숫자가 공백으로 구분되어 주어집니다.

세 번째 줄 부터는 $Q$ 개의 줄에 걸쳐 구간에 대한 정보 $a_i$, $b_i$ 값이 공백을 사이에 두고 주어집니다. 이는 주어진 $N$ 개의 숫자들을 $1$ 번부터 $N$ 번까지 순서대로 번호를 붙였을 때 번호가 \[$a_i$, $b_i$\] 구간에 있지 않은 숫자들 중 최댓값을 구해야 함을 의미합니다.

### 제한 조건

- $1 \le N, Q \le 100\,000$
- $1 \le \texttt{주어진 숫자 범위} \le 10^9$
- $1 \lt a_i \le b_i \lt N$

### 출력

$Q$ 개의 질의에 대해 각 구간 밖에 있는 숫자들 중 최댓값을 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
5 3
1 3 9 5 4
3 3
3 4
2 4
```

출력

```
5
4
4
```

예제 설명

접기

구간 $(3, 3)$ 에서 $3$ 번째로 주어진 정수 를 제외한 나머지 정수 중 최댓값은 $5$ 가 됩니다.

구간 $(3, 4)$ 에서 $3, 4$ 번째로 주어진 정수 를 제외한 나머지 정수 중 최댓값은 $4$ 가 됩니다.

구간 $(2, 4)$ 에서 $2, 3, 4$ 번째로 주어진 정수 를 제외한 나머지 정수 중 최댓값은 $4$ 가 됩니다.

밑의 그림에서, 각 구간을 순서대로 나타내었습니다.

![](https://contents.codetree.ai/problems/2213/images/problems-2ed38050-85b2-4d86-8433-59c4497f5df3.png)

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!