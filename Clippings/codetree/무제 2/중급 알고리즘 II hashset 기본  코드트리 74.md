---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-distance-11/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 사전순으로 가장 앞선 최단거리 경로

다익스트라 알고리즘을 사용하여 최단 거리로 이동하기 위한 경로를 구하기 위해서는 path라는 배열을 이용하면 된다고 했습니다. 그런데 만약 최단 거리를 만족하는 경로가 여러 개라면, 그 중 사전순으로 가장 앞선 경로를 찾기 위해서는 어떻게 해야 할까요? 사전순으로 앞서다는 말은 현재 위치에서 최단 경로로 이동할 수 있는 경우가 여러 가지라면, 그 중 정점의 번호가 가장 작은 경우를 선택해야 함을 뜻합니다.

이는 어떻게 해결해 볼 수 있을까요?

다음 그래프에서 알아보도록 하겠습니다.

![](https://contents.codetree.ai/problems/2250/images/introductions-6d390970-3228-4691-8add-69d221415d5d.png)

해당 그래프에서 1에서 5로 가는 최단거리는 6으로 `1->4->5` 도 가능하지만, 사전순으로 가장 앞선 최단경로는 `1->2->4->5` 가 됩니다.

이렇게 사전순으로 가장 앞선 최단경로를 구하기 위해서는 다음 과정을 거쳐 진행하면 됩니다.

1. 모든 간선을 뒤집고, 도착점(5번)을 시작점으로 하는 다익스트라를 진행합니다.
![](https://contents.codetree.ai/problems/2250/images/introductions-96eaffd4-222e-414d-bf35-3fc760c29075.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-28ba4a34-8713-4430-978b-ff55f36a1c05.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-57cc8905-8dbd-4084-a28f-c3dee34c84cd.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-176cbcab-b735-40c1-8927-e75d7fe5b2e2.png)

1 / 4

2. 시작점(1번)에서 출발하여 1번부터 N번까지 순회하며 **최단거리 경로 상에 존재할 수 있는 노드를 찾아** 이동하는 것을 도착점(5번)에 도달할 때까지 반복합니다. 이는 dist 값과 그래프의 간선값을 이용하면 확인이 가능합니다. 현재 위치를 x라 했을 때, `dist[i] + graph[i][x] == dist[x]` 인 정점 i번으로 계속 이동하면 실제 1번에서 5번으로 이동할 때의 최단경로로 계속 이동할 수 있게 됩니다.
![](https://contents.codetree.ai/problems/2250/images/introductions-cc91d028-e871-477e-a765-1f2270060208.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-909b3abb-a6ab-448f-9e86-2026d4ea1b92.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-1b744640-da1b-43df-a0fa-084b5666b49d.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-75400a32-a939-4f04-ac67-3f74933e4e8a.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-fbd022a2-bf24-4280-ad2e-4f87e060c2e2.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-dcd309b7-4e49-4cb5-a20c-bab086c2bba3.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-3a618403-3e08-4948-b298-31c93ed127d6.png) ![](https://contents.codetree.ai/problems/2250/images/introductions-c5e0999a-5d50-4f11-948e-ab427100579e.png)

1 / 8

코드는 다음과 같습니다.

```python
# 뒤집힌 그래프를 기준으로
# 도착지 1에서 시작하여
# 시작점 5가 나오기 전까지
# 최단거리를 만족하는 경로 중
# 가장 간선 번호가 작은 곳으로 이동합니다.
x = 1
print(x, end=" ")
while x != 5:
    for i in range(1, n + 1):
        # 간선이 존재하지 않는 경우에는 넘어갑니다.
        if graph[i][x] == 0:
            continue

        # 만약 b -> ... -> i -> x ... -> a로 
        # 실제 최단거리가 나올 수 있는 상황이었다면
        # i를 작은 번호부터 보고 있으므로
        # 바로 선택해줍니다.
        if dist[i] + graph[i][x] == dist[x]:
            x = i
            break

    print(x, end=" ")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.