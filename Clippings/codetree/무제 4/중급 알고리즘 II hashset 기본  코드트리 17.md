---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-minimum-spanning-tree-8/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Prim

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 프림 알고리즘

전체에서 간선을 선택하는 크루스컬과 반대로, 프림 알고리즘은 한 지점에서 시작하여 점점 확장을 진행하는 방법입니다. 다음 그래프를 이용하여 설명을 진행해보겠습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-542362cb-91ba-450c-be6f-b138930f9906.png)

프림 알고리즘은 아무 정점에서나 시작하면 됩니다. 편의상 1번 정점에서 시작해보겠습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-de745343-e2bd-488c-9fe3-799b00225db5.png)

이제 1번 정점에서 연결된 간선들 중 가중치가 가장 작은 간선을 고르면 됩니다. 따라서 가중치가 11인 간선이 선택되며, **이 간선이 MST에 들어가게 됩니다.**

![](https://contents.codetree.ai/problems/3395/images/introductions-3318e9d4-6716-498a-a524-f8c6a6af9553.png)

이제 MST를 이루고 있는 간선은 1-3 뿐입니다. 이 MST에 새로운 노드를 붙이기 위한 방법 중, 가중치가 가장 작은 간선을 고르면 1-2를 연결하는 가중치가 12인 간선 입니다. 그 간선을 골라 MST에 붙여줍니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-6af0b4a4-62df-4cc3-9082-cf3e7419d0f3.png)

그 다음 MST에 새로운 노드를 붙이기 위한 최소 가중치의 간선은 14입니다. 13을 붙여서는 안되는 이유는, 이미 MST에 포함된 노드끼리의 연결이므로 MST에 새로운 노드가 포함되는 것이 아니기 때문에 추가시 사이클이 발생하기 때문입니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-d1294cc2-0014-4f16-82ae-2fa8a5146d41.png)

이러한 과정을 계속 거치다보면, 모든 노드가 MST에 포함되었을 때 종료가 되며 저희가 구하고자 하는 MST의 모습이 확정됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-9e4639f8-262b-4b3f-87f2-ae5fe1e80539.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-ca4d6bc8-6cac-461b-877b-3652f5b7d861.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-edc927f0-0cfe-48ac-8036-9e789d302745.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-e3d8e19a-3710-4c49-b1c4-c12f5f9eebaf.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-2eee316d-380a-4a0a-965f-7acaad25d63b.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-54aead29-32c6-492c-944f-4b5273668e0b.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-cab3263c-a629-4cdb-a183-670fdb0f0fc8.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-0094ae85-c4ef-4b22-b3b1-4901997a151c.png)

1 / 8

이 과정에 대한 구현은 놀랍게도 다익스트라 알고리즘과 아예 동일합니다. 다익스트라 알고리즘의 경우, 현재 노드를 u라 했을 때 `dist[v]` 와 `dist[u] + length(u, v)` 를 비교하여 갱신해주는 것이였다면 prim은 단순히 `dist[v]` 와 `length(u, v)` 를 비교하여 갱신해주기만 하면 됩니다. 즉, 다익스트라 코드와 정확히 2줄만 다르고 나머지는 전부 동일합니다.

다음 그래프를 예로 프림 알고리즘을 설명해보겠습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-6a5a0fc5-ccbf-4b94-9295-73ec2ed30ee6.png)

프림은 시작점을 아무 점이나 잡아도 상관없다고 했습니다. 편의상 5번으로 잡고 시작해보겠습니다.

똑같이 dist 배열을 사용할 것이지만, 이 dist 배열의 정의가 다익스트라에서의 dist 배열과는 아예 다릅니다. `dist[x]` 는 **현재까지 만들어진 MST와 노드 x를 연결하기 위해 필요한 최소 비용** 입니다. 이 정의를 꼭 기억해주세요.

이제 다익스트라 알고리즘에서처럼 dist 배열을 초기화해주고 시작해보려 합니다. dist 배열을 전부 아주 큰 값(INF)으로 초기화하고, 출발지의 값만 0으로 설정하게 됩니다. 시작점만 0으로 설정해주는 까닭은, 처음 해당 노드가 선택되어야만 MST를 만드는 것을 시작할 수 있기 때문입니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-9169d1ca-8d55-40a3-86c2-50cd89871053.png)

이제 거리 dist 내의 값들 중 최솟값을 골라줍니다. 이렇게 최솟값을 골라주는 과정을 프림 알고리즘에서도 역시 여러 번 반복하게 되므로 우선순위 큐를 사용합니다. 따라서 우리는 처음 시작할 때부터 1번부터 5번 정점까지 전부 우선순위 큐에 넣어 거리 값 중 최솟값을 골라줄 수 있도록 합니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-de803240-850c-489c-9a9f-207b3d82f197.png)

처음 거리가 최솟값인 노드를 고르면 5번 노드가 선택됩니다. 이렇게 프림 알고리즘에서 최솟값이 뽑혔다는 의미는, 해당 노드를 MST에 추가하겠다는 뜻입니다. 이때 우선순위 큐에서 5번 노드는 빠지게 됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-a4972e96-8446-4043-9e78-f4fca7d85b8b.png)

이제 이 5번 노드에 연결된 노드들을 보며 간선에 적혀있는 값과 해당 노드에 적혀있는 dist값과 비교하여 더 작은 값으로 갱신해줍니다. 이 의미는, 현재 MST를 이루고 있는 노드가 5번 노드이므로 5번 노드에 추가적으로 연결할 수 있는 정점들에 대해 각 정점을 간선을 통해 추가했을 때 추가적으로 나가게 되는 비용을 갱신해주는 것입니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-0045aad3-0cd0-4c74-b745-6560ca26d067.png)

이 과정을 거치면 `dist[2]` 는 아주 큰 값인 INF였으므로 `length(5, 2)` 에 해당하는 값 4로 바뀌게 되며, `dist[4]` 역시 아주 큰 값인 INF였으므로 `length(5, 4)` 에 해당하는 값 2로 바뀌게 됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-cf9f100c-a3aa-4a7b-bd58-7bfdcd7533d2.png)

그 다음 우선순위 큐에 담겨있는 노드들 중 dist 최솟값을 갖고 있는 노드를 고르게 되면, `dist[4]` 값이 2 이므로 4번 노드가 골라지게 됩니다. 이때 이 의미에 주목해야 합니다. 이는 현재 MST에 4번 노드를 추가하는게 가장 좋은 상황이었다는 뜻으로, 이때 비용이 2만큼 든다는 뜻입니다. 따라서 다음과 같이 4번 노드가 뽑힘과 동시에 MST에 4-5를 연결하는 간선이 추가됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-e6d343c3-e725-49b8-9428-f80581e9c783.png)

4번 노드에 대해서도 연결된 간선들을 보며 최솟값으로 갱신해주는 작업을 거치게 됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-63c12d0f-508c-46a5-9adf-98be561403d4.png)

이 과정을 거치면 `dist[1]` 은 아주 큰 값인 INF였으므로 `length(4, 1)` 에 해당하는 값 3으로 바뀌게 되며, `dist[2]` 의 경우 원래 값이 4였지만, `length(4, 2)` 가 1로 더 작기 때문에 값이 1으로 바뀌게 됩니다. 또, `dist[3]` 의 경우 아주 큰 값인 INF였으므로 `length(4, 3)` 에 해당하는 값 2로 바뀌게 됩니다. 이 의미는 MST가 현재 노드 4, 5로 구성되어져 있는데 이들과 연결되기 위해 1번 노드는 비용 3이 필요하고, 2번 노드는 비용 1이 필요하고, 3번 노드는 비용 2가 필요하다는 뜻입니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-1a7d7a40-6881-401c-9642-3080bc632b95.png)

이때 4번 노드에 대해서만 갱신을 진행해도 되는 이유는 바로 다음과 같습니다.

현재 완성되어있는 MST는 다음과 같이 4-5로만 이루어져 있습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-b43dcdac-9499-438d-a7ff-1a0b15ad807d.png)

저희가 여기서 하고 싶은 것은 **현재 MST에 특정 간선을 새로 추가하여 새로운 정점을 하나 붙이고 싶은 것입니다.** 즉, 남은 정점에 대해 정점 4 혹은 정점 5에 연결하기 위해 필요한 최소 가중치의 간선 값을 구해야 합니다.

이때, 저희는 이미 정점 5에 대해서는 다음과 같이 5번에 새로 간선을 연결 했을 때의 최소 비용을 dist 배열에 적어줬습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-3aacc734-4601-477e-8f8a-66a65b434fd7.png)

따라서 4번 정점이 추가된 이후에는, 이제 4번 정점에 새로 간선을 연결 했을 때의 최소 비용을 dist 배열에 갱신해주면, dist 배열은 정점 4, 5 둘 중 하나에 연결하기 위해 필요한 최소 비용이 될 것입니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-bb8af7e9-c6c9-4cd7-a3ee-2c6a2e5bbc31.png)

그렇기에 이러한 과정을 모든 지점이 선택될 때까지 계속 반복하면, 최종적으로 dist 배열에 적혀있는 값들이 각 정점을 MST에 추가하기 위해 필요했던 최소 비용이 됩니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-28b416c6-f123-4cb0-88af-a3e35b99f692.png)

그래프 내의 정점의 수를 |V|, 간선의 수를 |E|라 했을 때 이 알고리즘의 시간복잡도는 다익스트라와 마찬가지로 $O(|E|log|V|)$ 가 됩니다. 그 이유는 프림 알고리즘을 진행하면 각 간선을 한 번씩 보게 되는데, 이때 dist값이 변하면 우선순위큐에서의 순서가 계속 바뀌게 될 수도 있으므로 간선의 수 $\times$ 우선순위 큐 이용 시간복잡도가 됩니다.

만약 우선순위 큐를 이용하지 않고, for 문을 이용해 최솟값을 찾는 식으로 코드를 구현한다면, 최솟값에 해당하는 노드를 고르는데 |V|번 시간이 소요되고 이 과정을 총 |V|번 반복해야 모든 노드를 선택하게 되므로 시간복잡도는 $O(|V|^2)$ 이 될 것입니다.

프림 알고리즘의 동작과정을 다시 한번 살펴보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-78cd1ea9-58fa-442a-a246-e08cdb996c60.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-c9ea2d75-0119-4e93-a51e-cae337a7a7c2.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-b876c994-e67c-42d8-8779-a9e5c1187e29.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-fcae84ea-beb3-413f-bf84-f039f63fb009.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-df07c19a-35e4-44cb-a2f8-a20edcbdb3f0.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-b3e5352a-608f-418d-b4b0-b9db7cd8e344.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-ac2bd604-e350-4001-b093-f7cff9fa7620.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-dfdbf63f-2912-43ec-8ae4-9c1dc38b5c59.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-4b863a02-1de2-4eea-8c2a-3824cd8e9c36.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-0cb30062-ed29-4031-bde8-afebb12739c1.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-1f149e36-3fa9-4a7d-87c2-8c70c7b996b4.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-d4b4c2b7-5d05-40d8-9949-d1488c42b37e.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-3e5a4f48-1464-4d65-be09-7e1f02c6c226.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-da8296e1-a851-42dd-a3da-3f78cc459829.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-9f61b465-5f6c-4ac4-b64e-8023cae0a700.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-3ef19996-e7ec-4723-befd-669ef93bd4bd.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-41df5c4a-fe68-4eea-91c2-f2e3b535e19b.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-8309a441-a120-4d44-a36c-b722090f94bc.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-c0ccd78f-90e1-4f53-9e3c-cfb3819023cb.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-4a2ea1d1-f68a-4ef3-9fb9-97ca920a1d62.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-809c19f0-9852-46da-bc8a-941fe1148f65.png)

1 / 21

프림 의사 코드를 살펴보면 다음과 같습니다.

```jsx
function prim(graph)                          // 그래프와 시작점 정보가 주어집니다.
    set Q = Queue()                           // 우선순위 큐를 만들어줍니다.

    for each vertex in graph                  // 그래프에 있는 모든 노드들에 대해
        set dist[v] = INF                     // 초기값을 전부 아주 큰 값으로 설정해주고 
        Q.push(v)                             // 우선순위큐에 각 노드를 넣어줍니다.
    set source = |V|                          // 시작점을 임의로 마지막 노드로 설정합니다.
    set dist[source] = 0                      // 시작점 대해서만 dist 값을 0으로 초기화해줍니다.
    while Q is not empty                      // 우선순위 큐가 비어있지 않을 때까지 반복합니다.
        set u = vertex in Q with min dist     // 우선순위 큐에서 dist값이 가장 작은 노드를 선택합니다.
        Q.remove(u)                           // 우선순위 큐에서 해당 노드를 제거해줍니다.

        for each neighbor v of u              // u번 노드와 연결된 노드들을 전부 살펴보면서
            set alt = length(u, v)            // 간선 가중치를 살펴봅니다.
            if alt < dist[v]                  // 기존 dist값보다 더 alt값이 작다면
                set dist[v] = alt             // dist값을 갱신해줍니다.
```

## O(∣V∣2)O(|V|^2) 알고리즘 구현

우선순위 큐를 이용했을 때 구현한 프림 알고리즘이 $O(|E|log|V|)$ 의 시간복잡도를 갖기 위해서는 꼭 그래프를 인접 리스트 형태로 관리해줘야 합니다. 이에 비해 우선순위 큐를 이용하지 않고 for 문을 이용해 최솟값을 찾는 식으로 코드를 구현하는 방법은 어차피 최솟값에 해당하는 노드를 고르는데 |V|번 시간이 소요되기 때문에 인접 행렬을 이용해도 됩니다.

따라서 여기서는 정점의 수에 해당하는 |V|가 작을 때 유용하게 사용되는 $O(|V|^2)$ 코드를 살펴보도록 하겠습니다.

먼저 인접행렬에 대해 간단히 알아보도록 하겠습니다. 인접 행렬은 두 정점 i, j가 연결관계에 있을 때 `graph[i][j]` 값을 1로, 그렇지 않다면 `graph[i][j]` 값을 0으로 정의하여 표현하는 방법입니다. 그 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/3395/images/introductions-95e90c2e-ca6b-4ab4-97a5-39f72ff3af11.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-8b932d52-e96b-453e-b116-0e6735a1290b.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-1252b86a-07ce-4931-aee6-847ce4fbe2f2.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-d98037f8-eb47-476b-86d4-0e6f5cc45ef6.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-54174e72-9a1b-4cb0-9a3f-ae06e2885190.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-12b4a5d6-8cdf-4924-9ebb-c87d5522a00e.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-e94b8863-7e11-4a48-a335-f2fbe9ee0058.png) ![](https://contents.codetree.ai/problems/3395/images/introductions-956c839f-3687-4d92-bebe-17e04705a7e7.png)

1 / 8

그래프에 가중치가 있는 경우에는, 1대신 해당 위치에 간선의 가중치를 적어주면 됩니다. 양방향 그래프라면 인접 행렬이 대칭인 모양이 되며, 단방향 그래프라면 그렇지 않을 것입니다. MST가 정의되기 위해서는 양방향 그래프여야 하기에, 단방향인 경우에 대해서는 크게 고민하지 않으셔도 됩니다. 그래프에서 정점의 수를 V, 간선의 수를 E라 했을 때 인접 행렬 이용시 공간복잡도는 $O(V^2)$ 이 됩니다.

이러한 인접행렬을 이용하여 다음 그래프에서 $O(|V|^2)$ 프림 코드를 구현해보면 다음과 같습니다.

$O(|V|^2)$ 프림 코드 구현시 dist중 최솟값을 갖고 있는 노드를 선택할 때, 이전에 선택되었던 노드가 다시 선택되지 않도록 visited 배열을 꼭 사용해야 함에 유의합니다.

```python
import sys

INT_MAX = sys.maxsize

# 변수 선언
# 정점의 수 : 5, 간선의 수 : 7인 그래프
n, m = 5, 7
graph = [
    [0] * (n + 1)
    for _ in range(n + 1)
]
visited = [False] * (n + 1)

# 그래프에 있는 모든 노드들에 대해
# 초기값을 전부 아주 큰 값으로 설정
dist = [INT_MAX] * (n + 1) 

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

# 그래프를 인접행렬로 표현
for i in range(1, m + 1):
    x, y, z = edges[i]
    graph[x][y] = z
    graph[y][x] = z

# 시작위치에는 dist값을 0으로 설정
dist[5] = 0

# O(|V|^2) 프림 코드
ans = 0
for i in range(1, n + 1):
    # V개의 정점 중 
    # 아직 방문하지 않은 정점 중
    # dist값이 가장 작은 정점을 찾아줍니다.
    min_index = -1
    for j in range(1, n + 1):
        if visited[j]:
            continue
        
        if min_index == -1 or dist[min_index] > dist[j]:
            min_index = j

    # 최솟값에 해당하는 정점에 방문 표시를 진행합니다.
    visited[min_index] = True

    # mst 값을 갱신해줍니다.
    ans += dist[min_index]

    # 최솟값에 해당하는 정점에 연결된 간선들을 보며
    # 시작점으로부터의 최솟값을 갱신해줍니다.
    for j in range(1, n + 1):
        # 간선이 존재하지 않는 경우에는 넘어갑니다.
        if graph[min_index][j] == 0:
            continue

        dist[j] = min(dist[j], graph[min_index][j])

# mst값을 출력합니다.
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.