---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-distance-9/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 최단거리 경로

다익스트라 알고리즘 (Dijkstra Algorithm)은 **특정 시작점** 에서 **다른 모든 정점** 으로 가는 최단거리를 각각 구해주는 알고리즘이라 했습니다. 그렇다면 특정 시작점에서 특정 도착점으로 최단거리로 이동하기 위한 경로는 어떻게 구해볼 수 있을까요?

그 방법은 바로 `path` 라는 배열을 하나 만들어, `dist[i]` 가 `dist[min_index] + graph[min_index][i]` 값으로 갱신되는 그 순간에 `path[i]` 에 min\_index를 넣어주는 것입니다.

path를 설정하여 다익스트라를 진행하면 다음과 같이 `path[i]` 에 시작점으로부터 **i번째 정점에** 최단거리로 도달하기 위한 **바로 직전 노드의 번호** 가 적히게 됩니다. 이때 `i <- path[i]` 로 이루어져 있는 간선을 전부 표시해보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/1868/images/introductions-522befd1-23ee-400e-8e26-89bf2cda3aad.png)

이렇게 색칠되어 있는 간선들은 다음 특징을 갖게 됩니다.

1. 사이클을 이루지 않습니다.

사이클을 이룬다면 최단거리가 될 수 없기 때문입니다.

2. 트리 모양을 띄게 됩니다.

사이클을 이루지 않으며, 모든 간선을 연결하고 있는 트리 형태를 띄게 됩니다.

3. 시작점으로부터 각 정점으로 해당 간선으로만 이동하여 최단거리를 만들어 낼 수 있습니다.

그렇다면 최단거리에 해당하는 경로는 어떻게 찾아낼 수 있을까요?

예로 위의 그래프에서 5번 정점을 시작으로 1번 정점에 다다르기 위한 최단거리 경로를 구해보겠습니다. **경로는 도착점을 시작으로 path배열을 이용하여 거꾸로 이동하여 거쳐가는 점들을 적어준 뒤, 최종적으로 리스트를 거꾸로 뒤집어 주는 식으로 찾을 수 있습니다.**

![](https://contents.codetree.ai/problems/1868/images/introductions-0dd1564b-98e6-40d8-b637-ed3a3ce740a8.png) ![](https://contents.codetree.ai/problems/1868/images/introductions-f8e9eca1-2ffa-477d-8119-497d1fe00667.png) ![](https://contents.codetree.ai/problems/1868/images/introductions-e598c005-8110-40c0-bd22-982f1f8c508d.png) ![](https://contents.codetree.ai/problems/1868/images/introductions-c7127296-e0a3-4e6d-a37c-4161b11f45e8.png) ![](https://contents.codetree.ai/problems/1868/images/introductions-87fd69dd-d2b8-4120-9705-31adf21305fc.png)

1 / 5

코드는 다음과 같습니다.

```python
# 다익스트라 코드 중 갱신 부분
...
    if dist[j] > dist[min_index] + graph[min_index][j]:
        dist[j] = dist[min_index] + graph[min_index][j]
        # path값을 갱신해줍니다.
        path[j] = min_index
...

# 경로 찾는 부분

# 도착지 1에서 시작하여
# 시작점 5가 나오기 전까지
# path를 따라 움직여줍니다.
x = 1
vertices = []
vertices.append(x)

while x != 5:
    x = path[x]
    vertices.append(x)

# 거쳐간 순서를 거꾸로 출력합니다.
for num in vertices[::-1]:
    print(num, end=" ")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.