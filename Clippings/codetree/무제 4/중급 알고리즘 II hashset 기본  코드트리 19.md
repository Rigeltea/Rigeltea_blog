---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-growing-edge-value/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Prim

## 커지는 간선의 값

Easy

30XP

평균 32분

52% 정답률

총 제출 119회

$N$ 개의 정점과 $M$ 개의 간선으로 이루어진 그래프가 있습니다.

모든 간선을 다 사용할 수는 없기 때문에, 간선을 적절하게 골라 가중치의 합을 최소로 하면서 모든 정점을 연결하려 합니다. $N$ 개의 노드끼리 연결이 전혀 되어 있지 않은 상태에서 사용할 간선을 하나씩 확정짓게 되는데, 간선을 하나 확정할 때마다 아직 확정되지 못한 간선들의 가중치는 동시에 $K$ 씩 올라갑니다.

모든 정점을 연결할 때, 연결한 모든 간선의 가중치의 합이 최소가 되도록 하려고 할 때, 가중치의 합을 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 정점의 개수 $N$, 간선의 개수 $M$, 증가하는 간선의 값 $K$ 가 공백을 두고 주어집니다.

두 번째 줄부터 $M$ 개의 줄에 걸쳐, 각 간선의 양 끝 점과 가중치가 공백을 두고 주어집니다.

### 제한 조건

### 출력

모든 정점을 연결하는데, 연결한 모든 간선의 가중치의 합이 최소가 되도록 하려고 할 때, 가중치의 합을 출력합니다.

### 입력 예제

### 예제 1

입력

```
4 5 5
1 2 3
1 3 1
1 4 1
2 3 1
3 4 3
```

출력

```
18
```

예제 설명

접기

예제 1번에서, $1$ 번 정점과 $3$ 번 정점을 연결합니다. 이 때 가중치의 합은 $1$ 입니다.

그 후, $1$ 번 정점과 $4$ 번 정점을 연결합니다. 이 때 가중치의 합은 $1+(1+5)$ 입니다.

그 후, $3$ 번 정점과 $2$ 번 정점을 연결합니다. 이 때 가중치의 합은 $1+(1+5)+(1+5+5)=18$ 입니다.

### 제한

• Time Limit: 2000 ms

• Memory Limit: 120 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!