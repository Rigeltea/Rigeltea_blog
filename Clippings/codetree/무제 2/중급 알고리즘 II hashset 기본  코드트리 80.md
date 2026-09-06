---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-shortest-round-trip/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Floyd Warshall

## 최단 왕복

Easy

40XP

평균 13분

59% 정답률

총 제출 319회

$N$ 개의 정점과 $M$ 개의 간선에 대한 정보로, 간선의 양 끝 정점과 해당 간선에 주어진 가중치가 주어질 때, 임의의 서로 다른 두 정점 사이를 왕복하는 데 이용하는 간선들의 가중치의 총합이 가장 낮은 경우를 구하는 프로그램을 작성하세요. 이때, 주어진 $N$ 개의 정점과 $M$ 개의 간선으로 만들어지는 그래프는 방향그래프가 됩니다.

### 입력

첫 번째 줄에 정수 $N$, $M$ 이 공백을 두고 주어집니다.

두 번째 줄부터 $M$ 개의 줄에 걸쳐 각 간선을 연결하는 두 정점의 번호, 해당 간선에 주어진 가중치를 나타내는 정수들이 공백을 사이에 두고 주어집니다.

### 제한 조건

- $1 \le N \le 100$
- $1 \le M \le N \times (N-1)$
- $1 \le$ 간선의 가중치 $\le 10\,000$
- 최소 한 개 이상의 정점은 왕복이 가능합니다.
- 동일한 간선은 여러 번 주어지지 않는다고 가정해도 좋습니다.

### 출력

첫 번째 줄에 임의의 두 정점 사이를 왕복하는 데 이용하는 간선들의 가중치의 총합 중 최솟값을 출력합니다. 최소 한 개 이상의 정점은 왕복이 가능합니다.

### 입력 예제

### 예제 1

입력

```
3 4
1 2 1
3 2 1
1 3 5
2 3 2
```

출력

```
3
```

예제 설명

접기

$2$ 번, $3$ 번 정점을 고르면 총 비용 3으로 왕복이 가능합니다.

![](https://contents.codetree.ai/problems/1839/images/problems-313c0292-cd8a-425f-b532-8e6871c961e5.png)

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!