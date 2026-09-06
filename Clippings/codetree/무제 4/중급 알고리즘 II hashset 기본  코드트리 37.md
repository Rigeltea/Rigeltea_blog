---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-bitonic-cycle/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Bitonic Cycle

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Bitonic Cycle

다음과 같이 5개의 노드와 10개의 가중치가 있는 양방향 간선으로 이루어진 그래프가 있습니다. 1번 정점에서 시작해서 정점 번호가 증가하는 순으로 고르다가 5번 정점을 찍고, 이후에는 정점 번호가 감소하는 순으로 정점들을 방문하며 최종적으로 다시 1번 정점으로 돌아오려고 합니다. 단, 모든 정점을 정확히 한번씩 방문하고 와야합니다(1번 정점만 예외적으로 2번). 이 경우 이동 경로의 합을 최소로 만들기 위해서는 어떻게 이동해야 할까요?

![](https://contents.codetree.ai/problems/3449/images/introductions-2714e0a6-3e48-48d9-8e84-c3e50f553262.png)

만약 1 -> 5 -> 4 -> 3 -> 2 -> 1 순으로 이동한다면 1 + 3 + 20 + 4 + 3 = 31에 모든 정점을 방문하고 돌아올 수 있게 됩니다. 하지만 만약 아래와 같이 1 -> 2 -> 3 -> 5 -> 4 -> 1 순으로 이동한다면 3 + 4 + 2 + 3 + 2 = 14 만으로 모든 정점을 방문하고 돌아오게 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-9c09dfe2-402a-47c3-8b00-30d526707d21.png)

만약 특별한 조건 없이 겹치지 않게 모든 정점을 단 한번씩만 방문하여 돌아오는 최단거리를 구하는 문제였다면 이는 유명한 TSP([Traveling Salesman Problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem)) 문제로 효율적인 풀이 방식이 존재하지 않습니다.

단, 위의 문제에서 처럼 선택되는 수가 계속 증가/감소해야 하는 등의 조건을 만족하며 끝까지 이동한 뒤 다시 조건하에서 처음으로 돌아오는 형태의 문제는 Bitonic Tour라고 부르며 이는 특별하게 정의된 DP 형태로 풀리게 됩니다.

우선 DP로 해결하기 위해 주어진 문제를 다음과 같이 바꿔보겠습니다.

```
1번 지점에서 동시에 2명이 출발하여 n번 지점으로 가는데 서로 겹치지 않게 번호가 증가하는 방향으로만
정점을 거쳐 가되 최종적으로 둘이 n번 지점에 도착했을 때 모든 지점을 빠짐 없이 
지나와야 한다는 조건 하에서 가능한 최소 이동 거리를 구해보시오.
```

이렇게 문제가 바뀌게 되더라도 위 문제에서의 답은 아래와 같이 14로 동일하게 구해집니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-169a6c14-1d7c-49c4-85e0-5d84e0ec00c3.png)

1번에서 n번을 찍고 다시 1번으로 오는 것이나, 1번에서 2명이 출발하여 동시에 이동하여 n번으로 도착하는 것이나 결국 똑같은 문제가 됩니다. 동시에 출발하여 이동하는 문제에서는 DP를 진행하기 위해 중요한 요소 중 하나인 `방향성` 이라는 것을 명확히 정의할 수 있기 때문에, 아래와 같이 정의를 세워볼 수 있게 됩니다.

`dp[i][j] = 둘 다 시작점에서 출발하여 서로 겹치지 않게 정점을 순서대로 빠짐없이 방문하여 현재 한 사람은 i번 정점에 있고, 나머지 사람은 j번 정점에 있는 상황이 되었을 때 가능한 최소 이동거리`

이제 여기서 점화식을 세우기 보다는 **뿌려지는 형태의 동적계획법** 을 진행해보려고 합니다. 보통의 동적계획법 문제는 점화식을 세워 작은 문제에 해당하는 이전 값들이 채워져있다는 가정 하에서 현재 상태에 해당하는 최적의 값을 계산하는 식으로 진행됩니다. 이러한 방식은 `이미 완성된 값을 가져오는 형태의 동적계획법` 입니다. 하지만 상황에 따라 가져와야 할 부분을 직관적으로 떠올리거나 정리하는 것이 어려운 경우가 더러 있습니다. 지금 이 문제에서는 점화식을 세워 가져오는 방법으로 진행하기보다는, **이미 값이 구해져있다는 가정 하에서 이 상태가 영향을 미치는 그 다음 상태를 찾아 값을 갱신해주는 식인** 뿌려지는 형태의 동적계획법을 진행해보려고 합니다.

`dp[i][j]` 값이 이미 구해져있다고 가정해보겠습니다. 즉, 정의상 아래와 같이 한 사람은 1번 정점에서 이동하여 결국 i번 정점에 서있고, 다른 사람은 1번 정점에서 이동하여 결국 j번 정점에 서있는 상황입니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-6885d4c2-eac0-4233-81d7-6fe788cc0940.png)

이때 관찰할 수 있는 부분은 문제 정의상 모든 정점을 방문해야만 하기에 **1번 정점부터 max(i, j) 위치의 정점까지는 이미 두 사람에 의해 전부 방문 되었다는 것을 전제로 해도 된다는 것입니다.** 즉, max(i, j) + 1값을 k라 했을 때 우리가 그 다음으로 이동해야만 하는 정점은 k번 정점입니다. 따라서 `dp[i][j]` 값이 채워져있다는 가정하에서 그 다음 k번 정점으로 이동하는 경우만 고려하면 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-175bd24e-452b-407d-be49-3b1d53cf56c5.png)

경우는 크게 2개로 나뉩니다.

첫 번째 경우는 i번 정점에 서 있던 사람이 k번으로 이동하게 되는 경우 입니다. 이 경우에는 추가적으로 이동하게 되는 거리인 dist(i, k)만큼이 더 추가되고, 두 사람이 서 있게 되는 위치는 각각 k, j가 되므로 `dp[k][j]` 에 대해 기존 `dp[k][j]` 값과 현재 `dp[i][j]` 로부터 새롭게 구해지는 값을 비교하여 최솟값을 갱신해주면 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-972b6689-abd9-4466-802c-5585d46e285f.png)

두 번째 경우는 j번 정점에 서 있던 사람이 k번으로 이동하게 되는 경우 입니다. 이 경우에는 추가적으로 이동하게 되는 거리인 dist(j, k)만큼이 더 추가되고, 두 사람이 서 있게 되는 위치는 각각 i, k가 되므로 `dp[i][k]` 에 대해 기존 `dp[i][k]` 값과 현재 `dp[i][j]` 로부터 새롭게 구해지는 값을 비교하여 최솟값을 갱신해주면 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-c1c00bb2-019c-4c91-8617-9fe140b9757c.png)

초기 조건은 두 사람 모두 1번 정점에서 시작했을 때 이동거리가 0인 상황인 `dp[1][1] = 0` 이 됩니다. 최솟값을 구하는 문제이므로 나머지 칸에는 초기값으로 전부 아주 큰 값을 적어주시면 됩니다.

이런 초기조건과 점화식을 활용하여 위 예시 그래프에 대해 답을 구하는 과정을 살펴보면 아래와 같습니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-c5dfc3b5-c49d-4adf-9f9f-d57eb5f5703b.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-7751378d-18f9-490c-bb25-3def87417a9d.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-2e5bbd51-e883-4c36-bfcf-78f91b4cee1f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-187a1ba8-87ad-4c83-bfa3-9bf07f6be8b5.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-24e2b358-1d7e-4ee9-bb5a-f56af9ce3aba.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-fa738bd7-489b-4c04-84be-ce8f9132bfaf.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-e3d73c5b-d492-4fc7-8aa3-f86bd169257b.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-2a24ff60-cf3e-4833-8dfa-d761438bd25e.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-5f272183-ca6f-47d0-aaa6-c5ae00f1e601.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-a5db0824-adcc-44a6-aba3-6ab1fa8c45a0.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-7cb88e2d-ee5a-4552-aa21-c6134038eb16.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-990c47b7-4c8c-466f-807c-14b558de33be.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-46f83112-1150-49c0-a9a6-68d2fef57e7c.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-16f9626e-e17d-41e4-a77a-2a82fea9d72f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-4b2fe45e-682f-4bdf-ba75-20e3783c37ee.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-822098c5-6a5e-4cfa-8db7-314a9850c147.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-2826ba05-6ab1-4306-a5b9-82974373653d.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-9da37fe7-9865-4c62-9e3d-62d04f584b2a.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-18290177-1e8e-4ccb-b371-205f0e834548.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-309772e0-bd42-4d8a-afe5-1ef30688fbab.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-11846ad0-7f7e-4a93-991f-32f1a41a8a52.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-f620213c-fa36-471a-b3ef-26ccba3fc839.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-1ab7a65d-5eee-4505-ae2b-f3da7e5251f6.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-e5f6124f-7fba-4066-8d8e-3a65a0531265.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-c6c79520-9850-423f-8a95-4d7d8222cc9d.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-0a2e3435-9908-4369-8fb4-981b11df113d.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-e92c4d2d-ed53-4208-8fe3-50715a9e1304.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-8a0c05af-7671-441d-a9c7-7821fc2d1592.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-bd83c44c-69ae-4167-b43e-3432f7ee2235.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-8b2f312f-f877-471c-9cd4-37b11c08ec6c.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-4d8462c1-3dad-40bf-873d-cee5f99d4726.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-5a8c87b7-4112-41fe-bd24-4504d53de501.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-b57963f6-05bf-43c6-af0f-a890ef812c50.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-d7fe7896-4a02-47ba-97bb-760144c3b07f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-470624a2-68bd-4cf5-9baf-06fbfb4f6f8e.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-a20d2cab-9030-4a4f-934e-25051c298ea8.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-a443c47f-1670-494f-9049-fa38855ec4d4.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-23ab40f4-c2bc-40c8-80bb-d99486f6f190.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-ed228b09-2d7c-42f1-82cf-5839de831526.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-eb6a736b-64b0-4594-a1b8-23c6c4817ac6.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-29ce420b-0741-42cf-9876-e80a7418a748.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-7c62efa5-6d0c-45fa-8c2d-1c28a33709d8.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-82f3203e-484d-4e9c-ae76-cd4fdea17aae.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-5c903d59-987f-4ef5-b263-583012f873b4.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-cee4b628-7623-44a3-9ec4-b50356416341.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-612aab0f-2079-4502-9f73-3a1b7687851e.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-b48a08c3-0bdd-43f0-87c8-8c62ad19396c.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-31cc0ffb-0c96-4a81-a170-2a0c71504712.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-c9a41009-9f76-48a4-9be7-34417b9b758a.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-c27890c4-c392-4bbb-b01d-09d7f017ebfe.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-0aab999c-0036-4684-bbe2-d15bb2838a17.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-925b1fdf-a11e-4b91-8c67-9136f165f650.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-09b835d9-a80b-4d2c-a8fe-c697edcb0a7f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-9227ed51-2fe0-447b-8101-4a20511bebb9.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-d14ff702-bc11-4dc0-92a2-f963b6d5f561.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-7b1b17d5-0438-451c-a429-7e15ab734743.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-1346ef9b-499b-4a04-b960-ca17746284e9.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-fd0d47bb-13b5-473a-809e-b9ab4ba56907.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-f5202660-1581-4318-9112-528fd44bee6c.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-fc0aa6db-1e98-430b-ac97-7842f09bd644.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-8b60d791-ea69-4766-bc46-a30f0f962f1d.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-eff5be47-3d3a-4e40-a4b4-f1da2807f942.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-ff53d6c5-52f3-49ed-879d-8ad9f212ca0b.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-5da80afc-68f0-4a6a-81c3-2852ee73fc1f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-bec0d39e-d452-4a25-a6e9-980ec0f8f29e.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-2f3b7c7e-e450-465a-930a-8caf694c79a0.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-c9ea76d6-2c94-4a84-9a1a-c28a91c09b0f.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-093b6c3d-c11f-4f1c-9606-5bc39e060c25.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-8d888f7c-cd38-4d48-9359-057f2b358a60.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-20396e7e-b218-4f1b-a138-796d05b4cee4.png)

1 / 70

답은 결국 둘 다 5번 정점에 도달해야 하므로 모든 i에 대해 i번 정점을 끝으로 5번 정점으로 이동시켜 얻을 수 있는 최소 거리인 $dp[i][5] + dist(i, 5)$ 중 최솟값을 구하면 답이 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-073912e4-d11b-4178-b4d0-c31ff24839b6.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-5db983ce-0254-457b-af0b-e1c95d5c1da5.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-da420b06-3bad-49e6-ad47-8ad1b3799ca8.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-7019ff1e-e11a-4e71-9dc7-63fe744d697c.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-0c9f5df5-f9be-4438-8bbe-19ede23ad019.png) ![](https://contents.codetree.ai/problems/3449/images/introductions-cdb5f575-fafa-47f3-9afe-0205eb9b5ad9.png)

1 / 6

위 그래프에서는 나올 수 있는 값 중 최솟값이 14이므로 답은 14가 됩니다.

![](https://contents.codetree.ai/problems/3449/images/introductions-4833ed74-554e-4878-802a-a474ef1391b0.png)

이 과정을 코드로 나타내면 아래와 같습니다.

```python
import sys

INT_MAX = sys.maxsize

# 변수 선언 및 입력:
# 정점의 수 : 5
n = 5

# dp[i][j] : 둘 다 시작점에서 출발하여 서로 겹치지 않게 점을 순서대로 선택하면서
#            하나는 i번 점에 있고, 나머지 하나는 j번 점에 있는 상황이 되었을 떄
#            지금까지 온 거리의 합 중 가능한 최솟값
dp = [
    [0] * (n + 1)
    for _ in range(n + 1)
]

# 거리 정보
dist = [
    [0,  0,  0,  0,  0,  0],
    [0,  0,  3, 10,  2,  1],
    [0,  3,  0,  4,  3, 15],
    [0, 10,  4,  0, 20,  2],
    [0,  2,  3, 20,  0,  3],
    [0,  1, 15,  2,  3,  0],
]

# 최소를 구하는 문제이므로 
# 처음에 dp값을 큰 값으로 설정합니다.
for i in range(n + 1):
    for j in range(n + 1):
        dp[i][j] = INT_MAX

# 초기조건을 설정합니다.
# Bitonic Cycle 유형에서
# 둘 다 시작점인 1번 점에 서있는 순간입니다.
dp[1][1] = 0

# 뿌려주는 dp를 진행합니다.
# 이는 이미 값이 구해져 있다는 가정 하에서
# 그 다음 값을 갱신하는 형태입니다.
for i in range(1, n + 1):
    for j in range(1, n + 1):
        # 하나는 i번 점에 있고, 나머지 하나는 j번 점에 있는 상황에서
        # 그 다음 점으로의 이동을 고민해야 합니다.

        # dp[i][j] 값이 구해져있다는 가정 하에서
        # 그 다음 상황에 해당하는 값을 갱신해야합니다.

        # Bitonic Cycle 유형의 특성상
        # max(i, j)까지는 이미 전부 해결했기에
        # max(i, j) + 1번 점을 고려해야 하는 순간입니다.
        next_index = max(i, j) + 1

        # 이미 next가 n + 1이면 더 이상 진행하지 않습니다.
        if next_index == n + 1:
            continue
        
        # i번 점을 next로 이동하는 경우입니다.
        # 이 경우에는 i번 점과 next점 간의 거리만큼 더 더해줘야 합니다.
        # 이 경우를 기존 값과 비교하여 최솟값을 적어줍니다.
        dp[next_index][j] = min(dp[next_index][j], dp[i][j] + dist[i][next_index])

        # j번 점을 next로 이동하는 경우입니다.
        # 이 경우에는 j번 점과 next점 간의 거리만큼 더 더해줘야 합니다.
        # 이 경우를 기존 값과 비교하여 최솟값을 적어줍니다.
        dp[i][next_index] = min(dp[i][next_index], dp[i][j] + dist[j][next_index])

# 여기서의 답은 둘 다 n번 점으로 도착했을 상황이므로
# 한 쪽이 n인 경우에 대해서 
# 다른 한 쪽을 n으로 바로 연결시켜주는 경우 중 최솟값을 구해줍니다.
# 문제 특성상 dp[i][j]는 dp[j][i]와 값이 같을 것이므로
# 답 계산시 한쪽만 고려해도 됩니다.
ans = INT_MAX
for i in range(1, n):
    ans = min(ans, dp[i][n] + dist[i][n])

print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.