---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-edge-given-by-matrix/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Floyd Warshall

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 각 지점에서 갈 수 있는 곳들

앞서 플로이드 워셜 알고리즘은 그래프가 주어졌을 때 모든 쌍에 대해 최단거리를 구해야할 때 유용하게 사용될 수 있다고 배웠습니다. 이 알고리즘은 결국 정점 A 에서 정점 B로 가기 위해 거쳐갈 수 있는 모든 곳들을 고려하여 그 중 최단거리를 구해준다는 것을 알 수 있습니다.

이 컨셉을 이용하면 비슷한 패턴으로 다음 문제를 해결해 볼 수 있습니다.

> 그래프가 주어졌을 때, 모든 쌍에 대해 정점 A -> 정점 B로 갈 수 있는 경로가 존재하면 1, 존재하지 않는다면 0으로 나타내기

![](https://contents.codetree.ai/problems/1831/images/introductions-fa845b50-4992-436c-a4f6-dc309753aaa7.png)

`graph[i][j] = i에서 j로 가는 방법이 있다면 1, 없다면 0` 이라 정의했을 때, 플로이드 워셜과 거의 동일한 구조를 갖게 하되 `graph[i][k], graph[k][j]` 가 모두 1인 경우에 `graph[i][j]` 가 1이 되도록 하면, $O(V^3)$ 만에 모든 쌍에 대해 `graph[i][j]` 값을 올바르게 채울 수 있게 될 것입니다.

그 코드는 다음과 같습니다.

```python
# 변수 선언 및 입력:
n, m = 5, 8
graph = [
    [0] * (n + 1)
    for _ in range(n + 1)
]

edges = [
    (-1, -1),
    (2, 1),
    (1, 4),
    (4, 2),
    (5, 2),
    (5, 4),
    (4, 3),
    (3, 4),
    (1, 3)
]

# x -> y 관계를 graph에 표시해줍니다.
for i in range(1, m + 1):
    x, y = edges[i]
    graph[x][y] = 1

# i -> i로는 갈 수 있다고 전부 표시를 해줘야 합니다.
for i in range(1, n + 1):
    graph[i][i] = 1

for k in range(1, n + 1): # 확실하게 거쳐갈 정점을 1번부터 N번까지 순서대로 정의합니다.
    for i in range(1, n + 1): # 고정된 k에 대해 모든 쌍 (i, j)를 살펴봅니다.
        for j in range(1, n + 1):
            # i -> k, k -> j로 가능 길이 있다면
            # i -> j도 가능하다는 뜻입니다.
            if graph[i][k] and graph[k][j]:
                graph[i][j] = 1

# 모든 쌍에 대한 이동 가능 결과를 출력합니다.
for i in range(1, n + 1):
    for j in range(1, n + 1):
        print(graph[i][j], end=" ")
    print()
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.