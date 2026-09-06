---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-point-on-a-three-dimensional-plane/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Kruskal

## 3차원 평면 위의 점

Hard

90XP

평균 105분

61% 정답률

총 제출 167회

$3$ 차원 좌표평면 위에 $N$ 개의 점이 존재합니다. 점과 점 사이에 선을 그어 모든 점을 연결하려고 합니다.

임의의 두 개의 점을 연결할 때 드는 비용은, 두 점의 $x$ 좌표의 차, 두 점의 $y$ 좌표의 차, 두 점의 $z$ 좌표의 차 중 가장 작은 값이라고 할 때, 모든 점을 연결하는데 드는 비용의 최솟값을 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 점의 개수 $N$ 이 주어집니다.

두 번째 줄부터 $N$ 개의 줄에 걸쳐 각 점의 좌표가 한 줄에 하나씩 주어집니다.

### 제한 조건

- $1 \le N \le 100\,000$
- $-10^9 \le \texttt{좌표의 크기} \le 10^9$

### 출력

모든 점을 연결하는데 드는 비용의 최솟값을 출력합니다.

### 입력 예제

### 예제 1

입력

```
4
5 12 12
5 0 0
15 0 15
-90 -90 15
```

출력

```
0
```

### 제한

• Time Limit: 6000 ms

• Memory Limit: 160 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!