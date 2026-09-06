---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-path-to-each-vertex/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## O(|E|log|V|) 다익스트라 알고리즘

우선순위 큐를 이용하면 다익스트라 알고리즘을 $O(|E|log|V|)$ 에 구현할 수 있다고 했습니다.

![](https://contents.codetree.ai/problems/1834/images/introductions-3980d0cb-ab84-4cbf-baf9-6f5ef1886616.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-40901b91-0ab1-4d57-872c-aea2b29d9133.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-cb152ab4-db65-497f-bb53-c092ceb57647.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-e18b30c3-b9ea-4363-b1e1-e3129123b4a2.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-9f48bc6d-5ec4-4fb7-944b-99429fcb5e33.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-e5b7afee-fa38-4648-9022-00afdf38e48e.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-70284397-6528-4f36-8ca9-ee1e83504497.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-52a5956f-e8df-4b9b-bb85-ccc177ab28f4.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-cf513808-5a87-40e4-b5d9-a2a137e7abe6.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-3f5b3a44-bfc1-4957-bfad-1965e310d8ee.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-9998c9d7-8ac2-42b1-947b-b35fbc14cee0.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-ee53a734-11d3-4add-a89a-5ffb133fc269.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-f3851958-97a0-49a4-97df-8784d21caa3d.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-7d55e128-98f9-4748-9f81-6ecac0ea56bc.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-7ad33c22-f353-44e5-a7aa-d1134e5d049d.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-85e58496-5e6f-4bc8-af46-1f67eb1e715b.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-3d6275a0-0be4-4fd6-bc82-0807b0a5cccb.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-2dbf3928-6b3c-4b06-85ae-382403920b4d.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5f53e473-70eb-418b-a299-8c75e1df51cb.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-10d75811-70a0-49e0-ab16-9f68817bfef7.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-1969bf60-6c83-4ee4-9704-2d4c58e8ed58.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-a04f2891-9425-4fb6-8917-18da332916c3.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-975449df-9375-4c0e-8200-0d34eecdd0e4.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-9e06a4e0-5479-403f-9d99-f70f40ffc9f0.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-f6e17628-6b28-49d3-a532-23e96f533b77.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5969230f-6faa-44fd-a7fa-a18118a2c504.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-da4d7520-4e3a-4eb4-900b-1839c1e61c7c.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-6647a4fa-e991-409d-a9ff-d4810f749ab9.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-0710a054-05aa-4e7a-8e84-b927e7772697.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-600b6471-9514-4187-94fe-38f422b69b56.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-58cb944a-e53c-4411-ad11-1fdb673cdca5.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-f7bc249a-5d0b-4ddb-b748-d3fad9730a00.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-dba312e8-ffac-40cd-be14-96f19708e220.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-515c7c39-ea90-4936-83cc-a45d9759d866.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-fcd15dde-d4d0-4d7e-8d5f-f9075e124af8.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-c001cc92-aeb0-480d-a236-f6da5f2c42fd.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-be792112-d573-439b-9350-81a00646f18f.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-63887d4c-2182-4582-840f-522785be300f.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5331cdd3-e6c6-4006-a1e5-c621fe59f485.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-b9d68d71-e494-4fbb-9929-21a8b2b256cc.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-b94df89d-80e3-43cc-b451-4b27d93de9b8.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-25ba19b2-7680-4578-ad4f-bf4c63ec2b53.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-bc8fa29a-a470-4c1f-bf3a-ed00899f27a3.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-41f97cd8-b8f2-42c5-9123-2d798c5037f7.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-04383d31-7df0-46b1-acd0-d0474e0a1904.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-dda70f3f-b4f2-4cd1-a9b7-63ca58a96a04.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-3c1d8ca3-ec47-43cc-8ddb-49fd2a47dcf4.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-42271b85-ffdb-44f6-bdd6-995a089636fa.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-0ec73189-7a4c-49b4-9521-a060f266ddbf.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5c4f6595-a413-49d2-a78e-f2e81282da6f.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-3fecfc40-276d-45a7-967b-5ead5181d051.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-0c92c86a-b6cb-48fa-8357-f0b201628cbc.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-bd3eeba0-f02f-4dbd-b742-6ebdfb7213a6.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5925c1b0-9299-4029-8a51-658166d93d09.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-421f3753-64b8-47a3-be1e-c8f0233c33f3.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-79ccb7b1-e9c5-42cd-bfdf-7101a3e5edf8.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5e399eee-1622-4816-bb06-3af1abb8b904.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-4c1cc45b-4a5a-4c77-b1a5-b6e35c143d63.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-9a2f8ec2-4fea-4de0-86ba-5f315bae6eb2.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-888eed04-68e4-44d5-b902-2a5c130281e1.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-d09f3b89-0c24-40f9-a7a7-847101eb7e06.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-80043db6-eb82-481e-8f40-a23595d4085b.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-efd97ac2-59ee-45ef-8248-353509082ff1.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-e41bf02a-b919-4c62-aff9-507c4a01a1f1.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-f4fdbf0f-0f0f-4624-837b-45beb2ad6f60.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-adb264a7-919d-4a38-ae94-c81d4731562a.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-52f5c7da-26d7-402f-8308-7145d953420e.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-9807dd75-1d1f-41c9-af7a-63eb18276bfe.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-ca5123dc-158c-47b0-8169-ccb67168b870.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-520407b1-41c3-43d4-8350-142e4ec77e8c.png) ![](https://contents.codetree.ai/problems/1834/images/introductions-5a7a332d-94fa-42a3-8591-ac586e5b85b6.png)

1 / 71

우선순위 큐를 이용했을 때 구현한 다익스트라 알고리즘이 $O(|E|log|V|)$ 의 시간복잡도를 갖기 위해서는 꼭 그래프를 인접 리스트 형태로 관리해줘야 합니다.

먼저 인접리스트에 대해 간단히 알아보도록 하겠습니다. 인접리스트는 **V개의 동적 배열** 을 만들어 그래프를 표현하는 방법입니다. i번째 정점에 해당하는 동적 배열을 `graph[i]` 라 한다면, `graph[i]` 에 해당하는 동적 배열에 정점 i에 연결된 모든 정점 번호가 들어가야 합니다. 그 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/1834/images/introductions-dd71c246-f085-47e0-bbfd-97beb16357b1.png)

인접리스트의 경우 V개의 동적배열을 관리하는 리스트 1개와, 각 간선별로 정점이 2개씩 동적 배열에 각각 추가되므로 공간복잡도는 $O(V+E)$ 가 됩니다. 그래프에 가중치가 있는 경우에는, 각 정점에 연결되어있는 정점과 간선의 가중치를 같이 쌍으로 저장하여 표현해주면 됩니다.

이러한 인접리스트를 이용하여 다음 그래프에서 $O(|E|log|V|)$ 다익스트라 코드를 구현해보면 다음과 같습니다.

$O(|E|log|V|)$ 다익스트라 코드 구현시 우선순위 큐 특성상 같은 노드에 대한 dist 값이 더 작아지면 같은 노드가 갱신된 가중치와 함께 새로 우선순위큐에 들어가게 될 수 있기 때문에, 우선순위큐에서 pop시 해당 노드의 가중치가 갱신되지는 않았는지를 체크하여 최신 자료가 아닌 데이터에 대해서는 continue를 통해 pass해 주는 코드를 작성해주어야 코드가 최적화가 됨에 유의합니다. 보다 자세한 설명은 코드를 참고 부탁드립니다.

![](https://contents.codetree.ai/problems/1834/images/introductions-a5b86786-550f-4e34-ad1d-847eb1dd7c14.png)

```python
import heapq
import sys

INT_MAX = sys.maxsize

# 변수 선언 및 입력:
# 정점의 수 : 5, 간선의 수 : 8인 그래프
n, m = 5, 8

graph = [[] for _ in range(n + 1)]
pq = []

# 그래프에 있는 모든 노드들에 대해
# 초기값을 전부 아주 큰 값으로 설정
dist = [INT_MAX] * (n + 1)

# 주어진 간선 정보 (x, y, z)
#               x -> y로 향하는 간선이 있으며, 가중치는 z 
edges = [
    (-1, -1, -1),
    (2, 1, 3),
    (1, 4, 3),
    (4, 2, 1),
    (5, 2, 4),
    (5, 4, 2),
    (4, 3, 2),
    (3, 4, 1),
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

# O(|E|log|V|) 다익스트라 코드
# 우선순위 큐에
# 원소가 남아있다면 계속 진행해줍니다.
while pq:
    # 가장 거리가 가까운 정보를 받아온 뒤, 원소를 제거해줍니다.
    min_dist, min_index = heapq.heappop(pq)

    # 우선순위 큐를 이용하면
    # 같은 정점의 원소가 
    # 여러 번 들어가는 문제가 발생할 수 있어
    # min_dist가 최신 dist[min_index]값과 다르다면
    # 계산할 필요 없이 패스해줍니다.
    if min_dist != dist[min_index]:
        continue

    # 최솟값에 해당하는 정점에 연결된 간선들을 보며
    # 시작점으로부터의 최단거리 값을 갱신해줍니다.
    for target_index, target_dist in graph[min_index]:
        # 현재 위치에서 연결된 간선으로 가는 것이 더 작다면
        new_dist = dist[min_index] + target_dist
        if dist[target_index] > new_dist:
            # 값을 갱신해주고, 우선순위 큐에 해당 정보를 넣어줍니다.
            dist[target_index] = new_dist
            heapq.heappush(pq, (new_dist, target_index))

# 시작점(5번 정점)으로부터 각 지점까지의 최단거리 값을 출력합니다.
for i in range(1, n + 1):
    print(dist[i], end=" ")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.