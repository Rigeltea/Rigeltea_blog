---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-minimum-spanning-tree-9/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Prim

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## O(|E|log|V|) 프림 알고리즘

우선순위 큐를 이용하면 프림 알고리즘을 $O(|E|log|V|)$ 에 구현할 수 있다고 했습니다.

![](https://contents.codetree.ai/problems/3396/images/introductions-0b185186-1cfd-4ec1-a441-7ffd56a21e78.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-8c6b1355-0743-4569-a37d-d68211cd5257.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-fb4f61c2-c6d0-4382-851e-e4ea8d9fb4c6.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-8d4b02ae-f495-41dd-91a4-c3bf6c439e2f.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-b333a9c0-2646-461c-83ee-36dd2be40d5a.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-1510860c-e284-4018-bc7f-70c04acc1aa5.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-8149b6fc-5db2-42a9-bfb8-212353e1e6ad.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-7d7f8430-5a42-45d9-8a2b-0f474f1e15f3.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-268e632b-ce10-44d5-9366-b4223cd3fba5.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-fcbd0540-a897-486c-9988-cd0808aab217.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-f2794c7e-1618-4ffb-b70a-c6f39c910150.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-c73537a3-e16f-444a-acd2-0813359ed760.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-f45a1e0c-33a4-4090-89d7-a95ae14633e8.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-f7e5b0b0-b47c-4097-9d3f-c659d0f219b1.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-e1deff39-7297-434e-bfd8-1b364f743d93.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-936ace38-0ead-4ef1-9d2d-56ddb33d0264.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-c00a2df6-d255-456d-a027-4ed48f2f5eae.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-2494bff8-ea11-4125-bf32-45158a1635ae.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-cbe02cdd-825c-4f10-9287-1e3d0372f518.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-b9599f4b-a50d-496d-b964-00ccc42fedb0.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-1d96e263-dc8e-421a-98cb-9eb5c03d9477.png)

1 / 21

우선순위 큐를 이용했을 때 구현한 프림 알고리즘이 $O(|E|log|V|)$ 의 시간복잡도를 갖기 위해서는 꼭 그래프를 인접 리스트 형태로 관리해줘야 합니다.

먼저 인접리스트에 대해 간단히 알아보도록 하겠습니다. 인접리스트는 **V개의 동적 배열** 을 만들어 그래프를 표현하는 방법입니다. i번째 정점에 해당하는 동적 배열을 `graph[i]` 라 한다면, `graph[i]` 에 해당하는 동적 배열에 정점 i에 연결된 모든 정점 번호가 들어가야 합니다. 그 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/3396/images/introductions-4e25cb57-9677-46e1-9a0c-56790c6d396c.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-0da5995e-a9fe-409c-9975-4b2756154af8.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-73d07dd6-900b-4c40-a5e9-7850168cf053.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-1ed257d1-4e3f-4628-a70d-ad34d1238b2f.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-50e1983e-b2b9-491f-b4df-c22200a48092.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-6ea7c6f6-f96b-40df-8f1f-3428722d4a7f.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-4494f94a-9c48-4250-80f5-7e5fd0176803.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-fc3a7dca-cec7-419b-94f8-025834f7f233.png) ![](https://contents.codetree.ai/problems/3396/images/introductions-17b280d9-cb7a-4eaf-bfcc-0174c330dc89.png)

1 / 9

인접리스트의 경우 V개의 동적배열을 관리하는 리스트 1개와, 각 간선별로 정점이 2개씩 동적 배열에 각각 추가되므로 공간복잡도는 $O(V+E)$ 가 됩니다. 그래프에 가중치가 있는 경우에는, 각 정점에 연결되어있는 정점과 간선의 가중치를 같이 쌍으로 저장하여 표현해주면 됩니다.

이러한 인접리스트를 이용하여 다음 그래프에서 $O(|E|log|V|)$ 프림 코드를 구현해보면 다음과 같습니다.

$O(|E|log|V|)$ 프림 코드 구현시 우선순위 큐 특성상 같은 노드에 대한 dist 값이 더 작아지면 같은 노드가 갱신된 가중치와 함께 새로 우선순위큐에 들어가게 될 수 있기 때문에, 우선순위큐에서 pop시 해당 노드가 이미 선택된 적이 있다면 continue를 통해 pass해 주는 코드를 작성해주어야 코드가 최적화가 됨에 유의합니다. 보다 자세한 설명은 코드를 참고 부탁드립니다.

```python
import heapq
import sys

INT_MAX = sys.maxsize

# 변수 선언 및 입력:
# 정점의 수 : 5, 간선의 수 : 7인 그래프
n, m = 5, 7

graph = [[] for _ in range(n + 1)]
pq = []

# 그래프에 있는 모든 노드들에 대해
# 초기값을 전부 아주 큰 값으로 설정
dist = [INT_MAX] * (n + 1)

visited = [False] * (n + 1)

# 주어진 간선 정보 (x, y, z)
# x <-> y로 향하는 간선이 있으며, 가중치는 z 
edges = [
    (-1, -1, -1),
    (2, 1, 2),
    (1, 4, 3),
    (4, 2, 1),
    (5, 2, 4),
    (5, 4, 2),
    (4, 3, 2),
    (1, 3, 6)
]

# 그래프를 인접리스트로 표현합니다.
for i in range(1, m + 1):
    x, y, z = edges[i]
    graph[x].append((y, z))

# 시작위치에는 dist값을 0으로 설정
# 여기서는 시작위치를 5번으로 가정
dist[5] = 0

# 우선순위 큐에 시작점을 넣어줍니다.
# 거리가 가까운 곳이 먼저 나와야 하며
# 해당 지점이 어디인지에 대한 정보도 필요하므로
# (거리, 정점 번호) 형태로 넣어줘야 합니다.
heapq.heappush(pq, (0, 5))

# O(|E|log|V|) 프림 코드
# 우선순위 큐에
# 원소가 남아있다면 계속 진행해줍니다.
ans = 0
while pq:
    # 가장 거리가 가까운 정보를 받아온 뒤, 원소를 제거해줍니다.
    min_dist, min_index = heapq.heappop(pq)

    # 우선순위 큐를 이용하면
    # 같은 정점의 원소가 
    # 여러 번 들어가는 문제가 발생할 수 있어
    # 이미 계산해본 적이 있는 경우라면
    # 바로 패스해줍니다.
    if visited[min_index]:
        continue

    # visited 값을 true로 바꿔주고
    # 답을 갱신해줍니다. 
    visited[min_index] = True
    ans += min_dist

    # 최솟값에 해당하는 정점에 연결된 간선들을 보며
    # 최솟값을 갱신해줍니다.
    for target_index, target_dist in graph[min_index]:
        # 현재 위치에서 연결된 간선으로 가는 것이 더 작다면
        new_dist = target_dist
        if dist[target_index] > new_dist:
            # 값을 갱신해주고, 우선순위 큐에 해당 정보를 넣어줍니다.
            dist[target_index] = new_dist
            heapq.heappush(pq, (new_dist, target_index))

# mst값을 출력합니다.
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.