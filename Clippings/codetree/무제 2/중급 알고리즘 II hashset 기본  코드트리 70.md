---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-path-to-each-vertex-3/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 다익스트라 알고리즘

다익스트라 알고리즘 (Dijkstra Algorithm)은 **특정 시작점** 에서 **다른 모든 정점** 으로 가는 최단거리를 각각 구해주는 알고리즘입니다. 즉, 5개의 정점이 있고 1번 정점에서 출발한다고 가정하면, 1번에서 2~5번으로 가는 최단거리를 구해주는 것 입니다.

우리가 다른 지점까지의 거리는 모르지만, A라는 지점까지 가는 최단거리는 확실히 안다고 가정해봅시다. 그렇다면 A를 거쳐 다른 지점을 갈 수 있다면, 우리는 현재 아는 정보로

> 특정 지점까지 거리 = A까지 가는 거리 + A에서 특정 지점까지 소요되는 거리

라고 추측할 수 있을 것 입니다.

다익스트라는 이 아이디어를 기반으로 설계된 알고리즘입니다.

조금 알고리즘이 복잡하기 때문에, 다음 그래프를 가지고 천천히 진행해보도록 하겠습니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-452460f5-3358-4daa-8854-1985a8a57711.png)

5번을 시작점으로 했을 때, 각 지점에 도달하기 위한 최단거리를 구한다고 가정해보겠습니다.  
그렇다면 다익스트라 알고리즘에서는, 거리 배열을 전부 아주 큰 값(INF)으로 초기화하고, 출발지의 값만 0으로 설정하게 됩니다. 시작점만 0으로 설정해주는 까닭은, 최단거리가 0임을 분명하게 알 수 있기 때문입니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-c8b7a1d0-af1f-457e-9810-a44e7b7896b8.png)

이제 거리 배열(dist) 내의 값들 중 최솟값을 골라줍니다. 이렇게 최솟값을 골라주는 과정을 다익스트라 알고리즘에서는 여러 번 반복하게 되는데, 이런 경우에 효과적으로 최솟값을 계속 찾아주기 위해서는 **우선순위 큐** 를 이용해야 한다고 했었습니다. 따라서 우리는 처음 시작할 때부터 1번부터 5번 정점까지 전부 우선순위 큐에 넣어 거리 값 중 최솟값을 골라줄 수 있도록 합니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-e1d5704c-6618-413f-9406-9c540a0b832e.png)

처음 거리가 최솟값인 노드를 고르면 5번 노드가 선택됩니다. 이렇게 최솟값이 뽑혔다는 의미는, 시작점으로부터의 뽑힌 노드까지의 최단거리는 확실히 정해졌다는 뜻이기도 합니다. 이때 우선순위 큐에서 5번 노드는 빠지게 됩니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-4de8dd4d-ba55-43c1-8a4d-c9b31605f108.png)

이제 이 5번 노드에 연결된 노드들을 보며 `dist[5]` 에 간선에 적혀있는 값을 더했을 때 해당 노드에 적혀있는 dist값과 비교하여 더 작은 값으로 갱신해줍니다.

이 과정을 거치면 `dist[2]` 는 아주 큰 값인 INF였으므로 `dist[5] + 4` 에 해당하는 값 4로 바뀌게 되며, `dist[4]` 역시 아주 큰 값인 INF였으므로 `dist[5] + 2` 에 해당하는 값 2로 바뀌게 됩니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-609c523d-29c4-4087-ac92-f3d2c981557e.png)

그 다음 우선순위 큐에 담겨있는 노드들 중 dist 최솟값을 갖고 있는 노드를 고르게 되면, `dist[4]` 값이 2 이므로 4번 노드가 골라지게 됩니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-4b11278f-3799-4d48-8bc8-7623537301b2.png)

4번 노드에 대해서도 연결된 간선들을 보며 최솟값으로 갱신해주는 작업을 거치게 됩니다.

이 과정을 거치면 `dist[3]` 는 아주 큰 값인 INF였으므로 `dist[4] + 2` 에 해당하는 값 4로 바뀌게 되며, `dist[2]` 의 경우 원래 값이 4였지만, `dist[4] + 1` 이 3으로 더 작기 때문에 값이 3으로 바뀌게 됩니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-4419975a-6e55-4d65-a812-c6c3706e7c13.png)

모든 지점이 선택될 때까지 이 과정을 계속 반복하면, 최종적으로 dist 배열에 적혀있는 값들이 5번 정점을 시작으로 하여 각 지점에 도달하는 최단거리가 됩니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-3eb7b3ae-bfdf-40a4-8f88-48017a63543e.png)

그래프 내의 정점의 수를 |V|, 간선의 수를 |E|라 했을 때 이 알고리즘의 시간복잡도는 $O(|E|log|V|)$ 가 됩니다. 그 이유는 다익스트라 알고리즘을 진행하면 각 간선을 한 번씩 보게 되는데, 이때 dist값이 변하면 우선순위큐에서의 순서가 계속 바뀌게 될 수도 있으므로 간선의 수 $\times$ 우선순위 큐 이용 시간복잡도가 됩니다.

만약 우선순위 큐를 이용하지 않고, for 문을 이용해 최솟값을 찾는 식으로 코드를 구현한다면, 최솟값에 해당하는 노드를 고르는데 |V|번 시간이 소요되고 이 과정을 총 |V|번 반복해야 모든 노드를 선택하게 되므로 시간복잡도는 $O(|V|^2)$ 이 될 것입니다.

다익스트라 알고리즘의 동작과정을 다시 한번 살펴보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-e1fc18a0-d595-44b0-9763-2ad25c4b38f9.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-fe784763-72b0-43d7-bb3a-da23b96c05e4.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-b982ebe3-f3ca-440e-9ffa-be7c344b4965.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-ae484267-9d9f-48cd-a752-869b65d19f80.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-10030a1b-9ee7-40d5-b265-7d386414b31b.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-038e5d2c-bc43-4476-903f-2b01bb467992.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-2e238b3e-24ec-4cbf-9bd3-7b435eda3cea.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-716ca2ed-00f1-423d-b193-c5a639687e42.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-4b3fca92-f3c2-442d-8ede-9cc08863c67c.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-274e0283-848a-4dd4-9d66-d6fb9a13d1a8.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-084569a7-744d-4e02-915b-afb83fb92e83.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-8bdcd525-a098-4ba1-ac8d-d7d24c411b3a.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-6d936897-1639-48ee-8214-c0f3c1c39550.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-512e3857-8016-45b7-9288-a11469a5fdfb.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f78eaaeb-c456-4d81-a950-3a7f0ce2fc34.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-43551305-ca85-475e-adbe-db781accfda1.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-c5b65842-078b-4605-9241-ecfceb80925e.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-3515066c-fce3-4f50-bb2c-441c20a82d71.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-193e0d45-b8ae-4aff-93ab-cc120af7b0b0.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-150bf667-e386-4cfc-803c-c2851b6f8001.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-8bf5b5ab-a451-4c9b-b8bd-72dade2340ff.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-b78f3315-1218-410c-942b-939783cdd1db.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-73b6ce0d-f7e8-4b32-aec7-339d73cf9ad0.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-c1ae7527-ce8a-4844-a940-a454665720e0.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-9470b1c8-4a5b-4a1f-ae35-3bd73c3860cc.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-dedd04a0-c142-4826-8df1-29fadf71f9b2.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-dce4ba64-f447-457d-a741-65e362b2cefe.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-cee35014-0708-4fe8-9f30-962b6b229972.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-2157b00d-0c5f-4c33-8401-e972d28188c1.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-620e520c-b19e-430b-9638-ca53d24ebcf5.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f7a1158a-74ce-4c78-bda0-aad361f7b0e1.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f0c2365f-8528-42f6-9e5f-5f5895ca5edf.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-8c0363e5-7361-445d-b169-467053d0c370.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-12ee82f6-4452-4df8-b5b0-69d8abffdbd6.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-d5136fee-dad2-4a1a-a6b2-59e6cbf4e931.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-99b88073-9b37-4b4d-813b-1baf32583d97.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-6af013b9-662f-48e2-926a-9eaa57e55765.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-7038426c-aa2c-4e47-9bee-04f2b6f572eb.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-a5781d21-532e-4fb3-a439-036daf9b773a.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-c1a3101c-babf-4df8-98a8-e70d3d097345.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-b418a325-aa52-4338-bc6f-0a0a72b7be52.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-373ec494-1ff5-4d3f-a904-ee54b5777384.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-a23ff899-70c2-436d-bca5-b61e89bb5d12.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-5b738e75-8180-4d3c-b40f-1313b41486a6.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-8c3f15da-20ee-4022-9f4d-ce6cd337b914.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f006f871-96ad-4fcf-ad77-d134dc3d7aeb.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-b44796de-a001-439c-815b-19c10a711716.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-cddd7ab5-7b3b-4ae1-ab01-a796ff3fba20.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-07d46648-0911-4b22-a80e-492676c99077.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-870d8378-5be4-4917-984e-2de014a30bba.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-851c102c-4d6d-4637-bcfe-1b3586dfd0fa.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f4a0af21-f804-489d-9b91-92522865ce29.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-e8d5d222-39a7-4292-99db-9fcbab69fa79.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-3ad79098-d245-4dd1-aec0-800005a768b0.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f02eb4a6-76a9-4230-a225-d165e63db8ce.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-05ac2fa0-d5e3-4072-a8bd-7b228bddcf41.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-3c3b5495-a4ab-48c5-b8c4-a391a9bcd140.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-ac772393-ccff-4ce0-8f7d-bb48c2629a78.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-33101f10-7987-4324-bc49-7a1a96de2d23.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-14f588a0-b9ad-4982-92a5-6c196fb85b96.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-7baf25b6-7dd8-40d6-8164-ece86805bf8e.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-3901d821-3273-4849-8f55-0e127314fcea.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-a5f75481-0238-46bd-b671-48b0bc1da141.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-f6257e41-1d5c-47ed-80a7-e28bc169558d.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-68335c67-d0b9-4d0d-922c-c6e25819d9dc.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-d528b7bf-0ad8-422a-9841-7e4e7120780f.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-7ebc6366-4f8c-49ef-999a-d7b8d3db5c4e.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-5eb03526-9fa5-4685-b39c-3258b929cebc.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-94eaecf7-4a19-4c91-9da8-123c4dd765f3.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-ea695e93-cadd-4abc-9b6f-9528cf883ab2.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-ff4940be-6d63-421e-9630-7c15c477c840.png)

1 / 71

다익스트라 의사코드를 살펴보면 다음과 같습니다.

```jsx
function dijkstra(graph, source)              // 그래프와 시작점 정보가 주어집니다.
    set Q = Queue()                           // 우선순위 큐를 만들어줍니다.

    for each vertex in graph                  // 그래프에 있는 모든 노드들에 대해
        set dist[v] = INF                     // 초기값을 전부 아주 큰 값으로 설정해주고 
        Q.push(v)                             // 우선순위큐에 각 노드를 넣어줍니다.

    set dist[source] = 0                      // 시작점에 대해서만 dist 값을 0으로 초기화해줍니다.
    while Q is not empty                      // 우선순위 큐가 비어있지 않을 때까지 반복합니다.
        set u = vertex in Q with min dist     // 우선순위 큐에서 dist값이 가장 작은 노드를 선택합니다.
        Q.remove(u)                           // 우선순위 큐에서 해당 노드를 제거해줍니다.

        for each neighbor v of u              // u번 노드와 연결된 노드들을 전부 살펴보면서
            set alt = dist[u] + length(u, v)  // 현재 dist값에 간선 가중치를 더한 값을 계산하여
            if alt < dist[v]                  // 기존 dist값보다 더 alt값이 작다면
                set dist[v] = alt             // dist값을 갱신해줍니다.
```

그런데 다음 그래프에서도 다익스트라 알고리즘이 올바르게 동작할까요?

![](https://contents.codetree.ai/problems/2249/images/introductions-15eaad76-6090-4b2a-bfb0-79ea7cc39d8e.png)

`dist[5]` 가 처음 잡히게 되어 `dist[2]` 가 1, `dist[4]` 가 2로 갱신되고, 그 다음 최소인 `dist[2]` 가 잡히게 되어 `dist[1]` 은 `dist[2] + 3` 인 4로 갱신이 될 것입니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-7965d7af-f8ed-409c-87db-9144cf262ade.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-aacbf341-6043-498f-aa49-2b2861965782.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-6a860f17-62ff-42e9-852c-f24f8e5232f8.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-c53977a6-6cc3-4272-8ae4-14d84a396dff.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-375da2a8-62a3-4692-b001-bfca0487811b.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-8008d6a1-50a4-40ed-911f-ac086b76c64c.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-075b4cf6-bae7-4048-96b5-165abc41df09.png) ![](https://contents.codetree.ai/problems/2249/images/introductions-1ec1aaec-880c-490b-a307-76d817e4ac8b.png)

1 / 8

하지만 5번 정점에서 1번 정점으로 가는 최단거리는 5 → 4 → 2 → 1 을 통해 가면 3만에 갈 수 있습니다. 이처럼 **음수 가중치가 있는 그래프** 에서는 다익스트라가 올바르게 동작하지 않을 수 있습니다. 그 까닭은, 다익스트라에서는 dist중 가장 작은 값을 골랐을 때 그 값이 확실한 최단거리라는 보장이 되어야 하는데, 음수 가중치가 있으면 다시 골라졌던 정점에 도달하는 dist값이 더 작아질 수도 있기 때문에 최단거리임을 보장할 수 없게 됩니다.

따라서 음수 가중치가 있을 때의 최단거리는 다익스트라를 이용해서는 절대 구할 수 없습니다.

## O(∣V∣2)O(|V|^2) 알고리즘 구현

우선순위 큐를 이용했을 때 구현한 다익스트라 알고리즘이 $O(|E|log|V|)$ 의 시간복잡도를 갖기 위해서는 꼭 그래프를 인접 리스트 형태로 관리해줘야 합니다. 이에 비해 우선순위 큐를 이용하지 않고 for 문을 이용해 최솟값을 찾는 식으로 코드를 구현하는 방법은 어차피 최솟값에 해당하는 노드를 고르는데 |V|번 시간이 소요되기 때문에 인접 행렬을 이용해도 됩니다.

따라서 여기서는 정점의 수에 해당하는 |V|가 작을 때 유용하게 사용되는 $O(|V|^2)$ 코드를 살펴보도록 하겠습니다.

먼저 인접행렬에 대해 간단히 알아보도록 하겠습니다. 인접 행렬은 두 정점 i, j가 연결관계에 있을 때 `graph[i][j]` 값을 1로, 그렇지 않다면 `graph[i][j]` 값을 0으로 정의하여 표현하는 방법입니다. 그 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-1046757a-b248-4bdb-ae18-df5fbf8b5a41.png)

그래프에 가중치가 있는 경우에는, 1대신 해당 위치에 간선의 가중치를 적어주면 됩니다. 양방향 그래프라면 인접 행렬이 대칭인 모양이 되며, 단방향 그래프라면 그렇지 않을 것입니다. 그래프에서 정점의 수를 V, 간선의 수를 E라 했을 때 인접 행렬 이용시 공간복잡도는 $O(V^2)$ 이 됩니다.

이러한 인접행렬을 이용하여 다음 그래프에서 $O(|V|^2)$ 다익스트라 코드를 구현해보면 다음과 같습니다.

$O(|V|^2)$ 다익스트라 코드 구현시 dist중 최솟값을 갖고 있는 노드를 선택할 때, 이전에 선택되었던 노드가 다시 선택되지 않도록 visited 배열을 꼭 사용해야 함에 유의합니다.

![](https://contents.codetree.ai/problems/2249/images/introductions-ab118dbb-6d56-44ed-bc1a-4fb39136fbc0.png)

```python
import sys

INT_MAX = sys.maxsize

# 변수 선언
# 정점의 수 : 5, 간선의 수 : 8인 그래프
n, m = 5, 8
graph = [
    [0] * (n + 1)
    for _ in range(n + 1)
]
visited = [False] * (n + 1)

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

# 그래프를 인접행렬로 표현
for i in range(1, m + 1):
    x, y, z = edges[i]
    graph[x][y] = z

# 시작위치에는 dist값을 0으로 설정
# 여기서는 시작위치를 5번으로 가정
dist[5] = 0

# O(|V|^2) 다익스트라 코드
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

    # 최솟값에 해당하는 정점에 연결된 간선들을 보며
    # 시작점으로부터의 최단거리 값을 갱신해줍니다.
    for j in range(1, n + 1):
        # 간선이 존재하지 않는 경우에는 넘어갑니다.
        if graph[min_index][j] == 0:
            continue

        dist[j] = min(dist[j], dist[min_index] + graph[min_index][j])

# 시작점(5번 정점)으로부터 각 지점까지의 최단거리 값을 출력합니다.
for i in range(1, n + 1):
    print(dist[i], end=" ")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.