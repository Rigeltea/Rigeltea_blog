---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-predecessor/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Graph DP

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Graph DP

아래 조건을 만족하는 장난감을 하나 만들기 위해 필요한 기본 부품의 수는 어떻게 될까요?

- 1번 부품은 기본 부품입니다.
- 2번 부품을 만들기 위해서는 1번 부품이 2개 필요합니다.
- 3번 부품을 만들기 위해서는 1번 부품 2개와 4번 부품 3개가 필요합니다.
- 4번 부품을 만들기 위해서는 1번 부품 1개와 2번 부품 2개가 필요합니다.
- 장난감을 만들기 위해서는 4번 부품이 4개와 3번 부품 1개가 필요합니다.

편의를 위해 장난감을 5번 부품으로 생각하여 각 부품을 1번 ~ 5번 노드로 놓고 그래프를 그려보겠습니다. 각 노드가 만들어지기 위해 필요한 부품의 수를 각 간선의 가중치로 나타내어 그려보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/1240/images/introductions-53f2e1bb-dde3-4c03-b348-860a10479022.png)

이 그래프에서 각 부품을 만들기 위해 필요한 1번 부품의 수는 아래와 같습니다. 따라서 답은 37이 됩니다.

![](https://contents.codetree.ai/problems/1240/images/introductions-951af8c4-10b1-41ca-887f-97ab31fc5014.png)

이는 DP를 이용하여 계산할 수 있습니다. 아직 동적계획법에 대해 잘 모르신다면 [DP](https://www.codetree.ai/missions/2/problems/fibonacci-number/introduction) 유형을 공부하시고 나서 다시 이 설명을 읽는 것을 추천드립니다.

`DP[i] : i번 부품을 만들기 위해 필요한 기본 부품의 수` 로 정의하여 해결합니다. i번 노드로 들어오는 방향에 해당하는 노드 번호를 $c_1, c_2, ..., c_k$, 각 간선에 적혀있는 가중치를 $w_1, w_2, ..., w_k$ 라 했을 때, 다음 점화식을 만족하게 됩니다. 정의상 i번 부품을 만들기 위해 필요한 각 부품을 위한 기본 부품의 수에 해당 부품이 필요한 개수를 곱해 이 모든 값을 더해주면 필요한 기본 부품의 수가 구해지기 때문입니다.

$$
DP[i] = DP[c_1] \times w_1+DP[c_2] \times w_2 +...+DP[c_k] \times w_k
$$

DP는 큰 문제를 풀기 위해 이미 풀려있는 작은 문제의 답을 이용하는 방식이기에, $DP[i]$ 값을 구하기 위해서는 그 전에 필요한 부품에 해당하는 DP값들이 미리 구해져 있어야 합니다.

**이는 위상정렬을 통해 쉽게 구현이 가능합니다.** 위상정렬은 선후관계 조건에 어긋나지 않는 순서를 구해주기 때문에, 이를 이용하여 위상정렬 순서에 맞춰 DP값을 갱신해주면 됩니다.

이 문제에서는 1번 노드는 기본 부품이므로 초기조건은 `dp[1] = 1` 이 되고, 이를 시작으로 하여 각 위상정렬 순서에 맞게 dp값을 채워주면 문제에서 원하는 답을 얻을 수 있습니다.

위 그림에서는 1, 2, 4, 3, 5라는 순서가 가능하며, 해당 순서대로 dp값이 갱신되면 아래와 같이 올바른 답이 구해집니다.

![](https://contents.codetree.ai/problems/1240/images/introductions-c6c6c3fb-0c0e-4978-83a4-f3d3f14cd2ca.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-4995363b-0262-4199-a4e7-f41abe94eaf7.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-1e224925-ea5d-411c-92ea-d7243d0c9c05.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-e61f6e37-52b1-42d8-99d6-d66d15768bd9.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-ca30e287-ad5c-4f2d-a30f-ae0861014da4.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-09cc17f5-cb6e-499b-86ec-b0b3faa701e4.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-83254bba-e386-47fd-982d-5eedd76bc171.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-af28b6c3-cfb5-497b-914a-b116fc9c4fe5.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-0bc33c7a-5dcf-4a2f-b8d6-151d296c72b2.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-8797b8d9-bad9-41b3-888c-a79dc535bd84.png) ![](https://contents.codetree.ai/problems/1240/images/introductions-8877d943-5f39-4099-afc6-e34a9dbc19ed.png)

1 / 11

이러한 답을 구해주는 코드는 아래와 같습니다.

```python
from collections import deque

# 변수 선언 및 입력:
# 정점의 수 : 5, 간선의 수 : 7인 그래프
n, m = 5, 7

edges = [[] for _ in range(n + 1)]

# 진입차수를 관리합니다.
indegree = [0] * (n + 1)

# dp[i] : i번 부품을 만들기 위해 필요한 기본 부품의 수
dp = [0] * (n + 1)

# 위상정렬을 위한 큐를 관리합니다.
q = deque()

# 주어진 간선 정보 (x, y, w)
# x -> y로 향하는 간선이 있으며, 가중치는 w
given_edges = [
    (-1, -1, -1),
    (1, 2, 2),
    (1, 4, 1),
    (1, 3, 2),
    (2, 4, 2),
    (4, 3, 3),
    (4, 5, 4),
    (3, 5, 1)
]

# 그래프를 인접리스트로 표현합니다.
for i in range(1, m + 1):
    x, y, w = given_edges[i]
    edges[x].append((y, w))

    # indegree값을 갱신해줍니다.
    indegree[y] += 1

# 시작 위치는 1번 정점입니다.
q.append(1)

# 초기 조건에 해당하는 경우입니다.
dp[1] = 1

# 위상정렬을 진행합니다.
# queue에 원소가 남아있다면 계속 진행합니다.
while q:
    # 가장 앞에 있는 원소를 뽑아줍니다.
    x = q.popleft()
    
    # x에서 갈 수 있는 모든 곳을 탐색합니다.
    for y, w in edges[x]:
        # dp값을 갱신해줍니다.
        dp[y] += dp[x] * w

        # 해당 노드의 indegree를 1만큼 감소시켜줍니다.
        indegree[y] -= 1

        # 비로소 indegree가 0이 되었다면
        # queue에 새로 넣어줍니다.
        if not indegree[y]:
            q.append(y)

# n번째 부품을 만들기 위해 필용한
# 기본 부품의 수를 출력합니다.
print(dp[n])
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.