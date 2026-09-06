---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-strange-bomb/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. 전처리

## 이상한 폭탄

Easy

40XP

평균 36분

56% 정답률

총 제출 656회

이상한 폭탄이 $N$ 개 있습니다. 이 이상한 폭탄은 각자에게 부여된 번호가 있고, 같은 번호가 부여된 폭탄끼리 거리가 $K$ 안에 있다면 폭발하게 됩니다. 폭탄의 개수 $N$, 특정 거리인 $K$, 그리고 폭탄을 나열한 순서가 주어지면, 폭발 할 폭탄중에 부여된 번호가 가장 큰 번호를 출력하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$ 과 $K$ 가 공백을 사이에 두고 주어집니다.

두 번째 줄부터 각 줄마다 폭탄의 순서가 주어집니다.

### 제한 조건

- $1 \le K \le N \le 200\,000$
- $0 \le \texttt{폭탄의 번호} \le 1\,000\,000$

### 출력

첫 번째 줄에 폭발 할 폭탄중에 번호가 가장 큰 번호를 출력합니다. 터지는 폭탄이 전혀 없다면 $-1$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
6 3
7
3
4
2
3
4
```

출력

```
4
```

예제 설명

접기

폭탄의 순서는 \[$7$, $3$, $4$, $2$, $3$, $4$\] 입니다. 이때, 거리 $3$ 이내에 있는 폭탄들은 전부 터지게 되므로 이 중 가장 큰 번호는 $4$ 번이 됩니다.

![](https://contents.codetree.ai/problems/645/images/problems-043ef03f-213a-4847-ae71-c92a17347eec.png)

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!