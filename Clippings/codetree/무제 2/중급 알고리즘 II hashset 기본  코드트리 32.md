---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-count-number-of-points-2/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Grid Compression

## 점 개수 세기 2

Hard

90XP

평균 180분

41% 정답률

총 제출 636회

2차 평면 상의 서로 다른 위치에 $N$ 개의 점에 주어졌을 때, $Q$ 개의 질의에 대해 각각 해당 직사각형 내 점의 개수를 출력하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ 과 $Q$ 가 공백을 사이에 두고주어집니다.

두 번째 줄 부터는 $N$ 개의 줄에 걸쳐 $2$ 차 평면 상 $N$ 개의 점의 위치 $(x,\ y)$ 가 공백을 사이에 두고 주어집니다.

세 번째 줄 부터는 $Q$ 개의 줄에 걸쳐 직사각형에 대한 정보 $x_1, y_1, x_2, y_2$ 값이 공백을 사이에 두고 주어집니다. 이는 $(x_1,\ y_1)$, $(x_2,\ y_2)$ 를 두 꼭지점으로 하는 직사각형 내에 있는 점의 개수를 세어야 함을 의미합니다.

### 제한 조건

### 출력

$Q$ 개의 질의에 대해 각 직사각형 안에 놓여있는 점의 개수를 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
3 2
-2 5
4 9
3 -3
-2 5 4 10
-3 -5 2 5
```

출력

```
2
1
```

예제 설명

접기

$1$ 번 직사각형 안에는 점 $(-2,\ 5)$, $(4,\ 9)$ 가 있고, $2$ 번 직사각형 안에는 점 $(-2,\ 5)$ 가 있습니다.

![](https://contents.codetree.ai/problems/2209/images/problems-f152f165-907e-405c-95c5-f68123759614.png)

### 제한

• Time Limit: 5000 ms

• Memory Limit: 512 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!