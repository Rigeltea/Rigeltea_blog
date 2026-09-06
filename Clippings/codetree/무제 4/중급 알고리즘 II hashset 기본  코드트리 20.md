---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-height-of-friends/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Topological Sort

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 위상정렬

다음과 같이 방향성 그래프가 주어져 있고, 각 노드가 하나의 일 이라고 생각해봅시다. 앞에 일이 끝나야만 뒤에 일이 진행될 수 있는 문제라면, 어떤 순서대로 작업을 진행해야 할까요?

![](https://contents.codetree.ai/problems/3397/images/introductions-eef62077-cfce-446c-819a-624d71f656f7.png)

예를 들어 위 그래프에서 가능한 순서중에 하나는 `1, 3, 4, 6, 2, 5, 7` 입니다. `1, 4, 3, 6, 2, 5, 7` 도 가능하므로 가능한 순서가 유일하다고는 말할 수 없습니다.

이렇게 가능한 순서들 중 하나를 뽑아주는 방법을 위상정렬이라 부릅니다. 위상정렬 방법에는 크게 dfs를 이용한 방법, in-degree를 이용한 방법 이렇게 2가지가 있습니다.

먼저 dfs를 이용한 방법부터 알아보도록 하겠습니다. 결론부터 얘기해보자면, dfs로 탐색을 진행하다가 더 이상 진행할 수 없는 노드가 되었을 때 그 순서를 기록하게 되면, 위상정렬은 그 순서의 역순이 답이 됩니다. 따라서 이는 stack을 이용하여 편하게 구현할 수 있습니다.

한 노드에서 갈 수 있는 정점이 여러 개라면, 작은 번호부터 방문한다고 가정하고 진행과정을 살펴보도록 하겠습니다. dfs 진행 중 퇴각하게 될 시 stack에 넣어주게 되고, 모든 탐색이 진행된 이후에는 stack에서 순서대로 값을 빼내어 적어준 순서가 바로 위상정렬 순서가 됩니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-fd09fe54-1755-441b-9cd5-0d1e2928fcf8.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a144e07b-bba5-48b3-8b3b-4c3909fd6e92.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a354a6d2-5b11-4a4b-a834-bff4d9e3f4fa.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-bcbcac39-c873-4510-abe9-f15cddeae98f.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-e5bc0168-b56d-446b-ac08-bbd9b8ea0133.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-f69e9272-a1bd-46e8-91b2-5e0ad02d2b53.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-697b1286-ade0-4e19-ae1a-f1931d3b9bd9.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-0a05669c-d178-4749-b9ca-a61e12e45847.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-ffce1ac3-5eb3-4393-9e5e-2d5e30d63e90.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-af28e764-5868-434f-89aa-25760daa88d1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-d64394af-aa06-475e-a613-f75977bfa270.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-70cf32aa-cf93-482f-ba7d-4b33995a2b3d.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-79883ba0-25a3-4dfb-811b-d77925167bd2.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-fd1675d9-5c3c-4a62-a460-e94ba9b83286.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-6902fa69-0039-48ac-9c1e-54e60846944c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a530c46c-ae4a-4e9b-8653-6a48e6fd9e70.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-e0dc6c15-5ea8-44c2-b333-2a9f26c49e24.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-2ad7df58-1290-4189-affc-3e169d1cbde5.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-c4659384-f0ea-40e6-afe6-7b017dfd22e0.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-5d550c4d-7297-4715-86c5-ada3f4ca850a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-d22a94f3-a1cf-4017-b730-a76ccfd213ee.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-34d46440-cb8e-4db2-ba43-59dd0082f387.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-8adb30e4-3f6a-4c88-9f2c-bc3cebb5cf6c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-5a70d17a-603d-4ba8-a586-de0e88d3ac5c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-de5effc2-00f6-4846-ae5c-999a9ca48174.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-fa3f2eca-6334-4883-8352-01e1a629f5d0.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a2d63a9d-1673-43a0-9423-b4a97c5a54cf.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-bb5b7bbd-74ee-4388-88ea-204f5e8527b1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-6d19b659-ecde-4105-a10f-f286a798baaa.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-b7a4ac54-f28f-41f4-b757-7e77ba59cb03.png)

1 / 30

위와 같은 그래프에서 번호가 다음과 같이 주어져 있는 경우라면 어떻게 될까요?

![](https://contents.codetree.ai/problems/3397/images/introductions-80d2668d-0ad9-4779-8da6-8227113f36b1.png)

dfs 탐색을 1번부터 시작한다면 다음과 같이 1, 5, 7에 대한 순서만 정해지고 탐색이 종료되고 말 것입니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-97237f73-41b7-4a17-ad18-b1652e4c6a57.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a154cf89-f8cb-450b-8572-6d8ed1eabb0e.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-1fe943b8-ab45-4bcd-9deb-4865157bcca2.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-fe63d84e-cbd7-43e2-a9e4-eae71f5ca41b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-f98e2109-aa23-4b6b-8433-c4ad2fd4f2d4.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-61ec75c3-9f81-4147-8fcf-e5a1f1aee07f.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-8b142a5a-8e73-4d3a-90c6-5663a77a4bc1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-eff2ffff-999a-4404-93e0-e4813819cc2a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-9d34fb88-0493-4f59-8a5a-f2504c675f93.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-e8cc05ff-7a28-4ad9-91c7-e32557db285d.png)

1 / 10

그렇다면 다시 2번 정점에서 시작하여 남은 정점들에 대해 동일한 과정을 진행해줘야 합니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-d2402a4b-1e85-4840-ac58-9137d21141d1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-743cab8b-b034-48f3-9571-4303be1a601f.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-392f5f3c-d5ae-4f6a-b97f-d59451c8cb1c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-22d2209a-683e-46d3-a051-8da493357689.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-56377db8-93ca-42b8-b506-0c011a5c5ee1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-dbec7135-53b7-49e4-b2dd-bb9bf3ba0c81.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-582f4e9d-0484-464c-a774-6fb3567ed243.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-73bdb368-2d5b-4e9c-b3d1-e59f7527008e.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-e10b6d4a-3391-4505-8e8d-7f8de1525b9b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-ef91222c-6fa9-44ad-8154-9e5702eff68c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-bfd06442-3c6a-40d8-929a-9a48cc32ab3b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-533be76e-92e5-4bdd-898e-dbce2bcdd04a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-148fda8c-3219-4892-a5a3-a1adeb45050b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-1e42ddcf-81e4-4f3f-9756-bef427c19b67.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-00ddb70f-9434-46c1-ac49-99d994504851.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-3109f35e-cc00-4c00-b186-a5b1d5957c87.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-81691ec1-85f9-44b8-8b85-4bd4b9fa54be.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-30db4dd1-d0dd-41bf-a606-838ebdfbb9a5.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-ffe66745-0c5a-4599-ad4b-83c7d9685bf1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-c7264867-5702-4562-9c45-8f89af29ca32.png)

1 / 20

이처럼 dfs를 이용한 위상정렬에서 가장 중요한 점은, **1번 정점부터 n번 정점까지 순서대로 보면서 아직 방문한 적이 없는 정점에 대해서는 전부 해당 정점을 시작점으로 하여 dfs를 추가적으로 진행해줘야만 한다는 것입니다.**

dfs를 이용한 위상정렬 진행시 각 정점과 각 간선을 한 번씩 보게 되기에 시간복잡도는 $O(V + E)$ 가 됩니다.

처음 주어진 아래 그래프에 대해 dfs를 이용한 위상정렬 코드를 작성해보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-87b2c900-c76c-447d-9aac-c10a66f912d2.png)

#### 코드

```python
# 정점 7개, 간선 8개인 그래프
n, m = 7, 8
edges = [[] for _ in range(n + 1)]
visited = [False] * (n + 1)
reversed_order = []

# 주어진 간선 정보 (x, y)
# x -> y로 향하는 간선이 있다는 뜻
given_edges = [
    (-1, -1),
    (1, 2),
    (1, 3),
    (1, 4),
    (3, 6),
    (3, 5),
    (6, 2),
    (2, 5),
    (5, 7)
]

# 그래프를 인접리스트로 표현
for i in range(1, m + 1):
    x, y = given_edges[i]
    edges[x].append(y)

# DFS 탐색을 진행합니다.
def dfs(x):
    # x에서 갈 수 있는 모든 곳을 탐색합니다.
    # 단, 방문한 적이 없는 경우에만 진행합니다.
    for y in edges[x]:
        if not visited[y]:
            visited[y] = True
            dfs(y)

    # 퇴각 직전에
    # 현재 노드 번호를 넣어줍니다.
    reversed_order.append(x)

# DFS 탐색을 진행합니다.
# 단, 방문표시가 되지 않은 모든 곳을 시작으로 하여
# DFS를 진행해야 합니다.
for i in range(1, n + 1):
    if not visited[i]:
        visited[i] = True
        dfs(i)

# 위상정렬 순서대로 출력합니다.
# 거꾸로 출력해주면 됩니다.
for num in reversed_order[::-1]:
    print(num, end=" ")
```

그 다음으로는 in-degree를 이용한 방법을 알아보겠습니다. in-degree란 정점마다 해당 정점으로 들어오는 간선의 수를 의미합니다. 예를 들어, 다음 그래프에서 각 노드마다의 in-degree를 표시해보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-693da322-8341-45b6-9817-e1174222d5ab.png)

위상정렬이라는 것은 곧 앞에 처리해야 할 순서가 끝나고 난 뒤에 현재 일을 처리하면 되는 것이기 때문에, **in-degree가 0** 인 지점이 항상 시작점이라고 얘기할 수 있다는 것이 핵심입니다. 이때, in-degree를 이용한 위상정렬 방법에서 역시 한 노드에서 갈 수 있는 정점이 여러 개라면, 작은 번호부터 확인한다고 가정하고 진행과정을 살펴보도록 하겠습니다.

위의 그래프에서 in-degree가 0인 지점을 전부 queue에 넣고 시작합니다. 이 그래프에서는 1번 정점만이 처음 in-degree 값이 0이므로 1번 정점을 queue에 넣어주게 됩니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-fc6df52c-e779-4f9c-b6cb-c1b014ab3d55.png)

이제 queue에서 가장 앞에 있는 값을 뽑아, 해당 정점에 연결되어 있는 모든 간선을 살펴봅니다. 이때, 해당 간선이 가리키는 곳에 있는 정점의 in-degree를 1 감소시켜줍니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-e719f9ec-20e3-45a2-9cac-6fae580fe064.png)

간선을 직접 지워주지는 않지만, in-degree를 1만큼 감소시켜줬으므로 의미상 해당 간선은 지워진 것과 다름 없습니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-89ecb140-2f5e-4ada-ac59-2bda3c6a5400.png)

그 다음 1과 3일 잇는 간선 때문에 노드 3의 in-degree는 0이 됩니다. 이렇게 in-degree가 0이 된 순간에는 해당 노드를 바로 queue로 삽입해줍니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-31c95e0d-0bac-411e-aec0-f818d3c073be.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-c0e8fce8-eced-4ce2-be33-330f26d97205.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-eb4bf14e-1959-4c74-81f3-cf8640d1a77c.png)

1 / 3

노드 1에 대해서 연결된 간선을 전부 살펴보면 다음과 같이 됩니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-bfe37f25-a825-408f-8719-8cd84ff49135.png)

이제 큐가 비어지기 전까지 계속 과정을 반복하면 됩니다. 이러한 과정을 반복하며 큐에서 나온 그 순서가 바로 위상정렬 순서가 됩니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-a4840fb1-a733-4627-80dc-c4c5d7fb3b5e.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-9ba9975f-6109-4cdf-87bf-cc850360e21a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-87dec26a-a96b-4da8-9960-789b0032280d.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-9fef942f-8e06-41e0-a02f-28b7df5f3b3a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-33e81ee7-c702-4440-aeab-ac594b386039.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-b4df94b0-c6bd-4892-ac55-3ace2cdb3ed2.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-79ea3230-d8ca-4095-bb77-9072e77a206e.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-1d157b04-87f9-4c6e-8348-b0031f5c6c13.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-b5196a7b-1352-406a-9239-67d52726d48e.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-abba87fc-0232-41bc-96a8-361ecc15695c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-312b2d28-6d66-4902-a972-04172cd34879.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-fd70f01e-9993-4c37-ab5a-d6f150493e7b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-40dedecd-41d4-4625-b7ac-35bc0dc8b3b4.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-a7831cce-c010-4930-86cc-e7217deee5a4.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-acc04220-7561-4073-94ac-dd0aa8a5921c.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-c7f4c39b-c300-4441-923b-b32a8c123991.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-8b669609-eb4f-4508-8ace-acfad12c74af.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-bbdc8e7b-370f-42c1-aec1-42fcdcf57004.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-bcd05513-a94d-4a20-9537-10e91ffde98d.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-cb7f964f-e5ee-40f8-80bc-c6fbb9d45bbd.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-553f33b0-9602-4fd6-bc4c-ee4cdc3e53dd.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-466c277c-aaad-4093-88cb-00c6889c7033.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-21d576eb-d896-47a8-a7fd-05b6050ed3f1.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-7621bd2f-733f-463e-952a-94d8b27ca47a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-5b2199c5-65ae-43b0-8163-93273d52717b.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-9da42005-9476-4d1c-b968-eab9b830253a.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-6298f7ed-9da1-420b-a0fb-337c3e22ead9.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-132a3374-9c1c-437f-8943-e6fbe9ac0302.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-121c42ba-3eeb-47c7-a8cd-c31b82a0f719.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-647e27a3-c054-4619-8dd3-7ae4bdf6c419.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-564e93b0-9bc2-429a-a2c8-dce2394a325f.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-82cfee43-777d-49ac-acef-ac9598f4f1d9.png) ![](https://contents.codetree.ai/problems/3397/images/introductions-cb05576e-b5e7-4333-853a-1f5b3254f21d.png)

1 / 33

다음과 같이 in-degree가 0인 지점이 여러 개인 경우에도, 처음 queue에 여러 노드를 넣고 시작하는 것만 다를 뿐 다른 과정은 전부 동일합니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-b2a28342-d000-485a-8e93-c92f117f8775.png)

in-degree를 이용한 위상정렬 방법 역시 각 정점과 각 간선을 한 번씩 보게 되기에 시간복잡도는 $O(V + E)$ 가 됩니다.

아래 그래프에 대해 in-degree를 이용한 위상정렬 코드를 작성해보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-87b2c900-c76c-447d-9aac-c10a66f912d2.png)

#### 코드

```python
from collections import deque

# 정점 7개, 간선 8개인 그래프
n, m = 7, 8
edges = [[] for _ in range(n + 1)]

# 진입차수를 관리합니다.
indegree = [0] * (n + 1)

# 위상정렬을 위한 큐를 관리합니다.
q = deque()

# 주어진 간선 정보 (x, y)
# x -> y로 향하는 간선이 있다는 뜻
given_edges = [
    (-1, -1),
    (1, 2),
    (1, 3),
    (1, 4),
    (3, 6),
    (3, 5),
    (6, 2),
    (2, 5),
    (5, 7)
]

# 그래프를 인접리스트로 표현
for i in range(1, m + 1):
    x, y = given_edges[i]
    edges[x].append(y)

    indegree[y] += 1 # 진입차수를 갱신합니다.

# 처음 indegree 값이 0인 곳이 시작점이 됩니다.
# 이 노드들을 queue에 넣어줍니다.
for i in range(1, n + 1):
    if not indegree[i]:
        q.append(i)

# 위상정렬을 진행합니다.
# queue에 원소가 남아있다면 계속 진행합니다.
while q:
    # 가장 앞에 있는 원소를 뽑아줍니다.
    x = q.popleft()
    
    # x값을 출력합니다.
    # 뽑히는 순서가 곧 위상정렬 순서가 됩니다.
    print(x, end=" ")

    # x에서 갈 수 있는 모든 곳을 탐색합니다.
    for y in edges[x]:
        # 해당 노드의 indegree를 1만큼 감소시켜줍니다.
        indegree[y] -= 1

        # 비로소 indegree가 0이 되었다면
        # queue에 새로 넣어줍니다.
        if not indegree[y]:
            q.append(y)
```

무방향 그래프에서는 순서가 정의되지 않다보니 위상정렬 알고리즘을 적용하기가 어렵습니다. 또, 다음과 같이 사이클을 이루고 있는 경우 역시 순서를 정의할 수 없기 때문에 위상정렬을 적용할 수 없습니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-49e6712c-5a4b-4796-9f69-325a69377c7c.png)

또한, 비 연결 그래프의 경우에서 역시 위상정렬이 올바르게 정의됩니다. 이 경우 역시 dfs를 이용한 위상정렬과, in-degree를 이용한 위상정렬 방법이 모두 가능합니다.

![](https://contents.codetree.ai/problems/3397/images/introductions-bf959bd7-545d-4a31-a5fd-8eb35203f0c1.png)

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.