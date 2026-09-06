---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-path-to-each-vertex-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Floyd Warshall

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 플로이드

## 플로이드 워셜 알고리즘

가끔은 모든 지점의 거리를 알 필요가 있습니다. 그러나 다익스트라의 경우 한 지점에서 다른 지점으로 가는 최단거리만 제공하기 때문에, 모든 지점의 거리를 확인하기 위해선 각각의 지점에 대해 다익스트라를 한번 씩 돌려야 합니다. 굉장히 번거롭죠. 정점의 수를 V, 간선의 수를 E라 했을 때 다익스트라를 이용하여 한 시작점으로부터 다른 지점들 까지의 최단거리를 구하는데 시간복잡도가 간단한 방법으로는 $O(V^2)$, 우선순위 큐를 썼을 때는 $O(ElogV)$ 이었습니다. 이때 만약 모든 쌍에 대해 최단거리를 구하고 싶다는, 시작점을 모든 정점에 대해 지정해줘야 하므로 총 V번이 되어 시간복잡도는 $O(V^3)$ 혹은 $O(VElogV)$ 가 될 것입니다.

만약 그래프에 간선이 굉장히 많은 경우라면 $E=V^2$ 이 되므로, 이런 경우라면 $O(V^3)$ 이 더 효율적일 것입니다.

이처럼 모든 쌍에 대해 최단거리를 구해야하는 상황에서 사용하기에 아주 좋은 알고리즘이 존재하는데, 우리는 이것을 플로이드 워셜 알고리즘 (Floyd-Warshall Algorithm) 이라고 부릅니다.

아이디어는 다익스트라와 다소 유사한데, A → B로 가는 경로보다 A → X → B로 가는 경로가 더 짧다면 그것으로 갱신을 해주는 것입니다.

다음 그래프를 예시로 플로이드 워셜 알고리즘을 한번 진행해보도록 하겠습니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-404470c7-16a6-43cf-a176-7859690c3069.png)

먼저 $V^2$ 크기의 배열(dist) 내에 있는 모든 값을 최댓값은 INF로 채워줍니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-07dc82a9-6500-4db4-80a0-a04f088ac994.png)

이후 주어진 그래프에서 각 간선에 적혀있는 숫자들을 dist 배열에 적어줍니다. 단, `dist[i][i]` 는 자기 자신으로 가는 최단거리 이므로 값 0을 꼭 적어줘야만 합니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-f048e1a8-be16-4193-8389-9fc7a50de368.png)

그 다음부터는 노드 1부터 시작하여 N번 노드까지 순서대로 경유했을 때를 가정합니다.  
먼저 모든 쌍 (i, j)에 대해 노드 1을 경유하는 것이 더 좋은 경우 그 값을 갱신해줍니다. 즉, `dist[i][j] > dist[i][1] + dist[1][j]` 를 만족하는 경우 `dist[i][j]` 에 `dist[i][1] + dist[1][j]` 값을 넣어줍니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-f94f52b9-222f-4e4e-a763-afc0441cddc2.png)

다음 2번 노드에 대해서도 해당 노드를 경유하는 것이 더 좋은 경우 그 값을 갱신해줍니다. 즉, `dist[i][j] > dist[i][2] + dist[2][j]` 를 만족하는 경우 `dist[i][j]` 에 `dist[i][2] + dist[2][j]` 값을 넣어줍니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-dca46e08-d59d-4965-8d11-b28bffa7fbaf.png)

이렇게 N번 노드까지 전부 진행하게 되면, dist 배열에 각 쌍에 대한 최단거리가 남게 됩니다.

![](https://contents.codetree.ai/problems/1838/images/introductions-37c0b1c9-a8c1-4cd4-8ba4-9f2b3823c7e1.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-0a24cea5-def4-4e53-8cb1-39be04e55249.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-e46c9872-d4cd-479a-a25d-95f6ecc80802.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-bd5e2ba6-aaff-4d78-bbec-e6c0145a09e8.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-a37958f1-77c9-4360-a16e-97929cb27fa2.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-de56a520-b87c-4013-8e69-0ef0cda9601b.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-62b9f076-9419-432d-8219-f57b2e3b5048.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-7113d878-2e51-4ba6-b42e-ddc5f14a2fa6.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-9d952ae4-a5b7-4f91-900d-d10722a468fe.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-187f5057-a166-4d31-ba6a-0b2ae00c851d.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-969c16b4-94b4-45bb-853f-27a7b376a1f7.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-46663bcf-5487-4c5d-9586-1c782c600796.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-bf8005bd-6f8d-4169-90f9-3db937c762f0.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-3b95477a-c341-4353-9d72-013116d562bf.png) ![](https://contents.codetree.ai/problems/1838/images/introductions-b3a9b730-b29c-41c5-9faf-960baba13cb4.png)

1 / 15

요약하자면, 플로이드 워셜 알고리즘은 경유할 점을 1번 노드부터 N번 노드로 확장해가며, `dist[i][j]` 가 `dist[i][k] + dist[k][j]` 보다 크다면 갱신해주는 방식입니다. 이때 for문 순서를 k, i, j가 아닌, i, j, k로 하면 제대로 된 최단거리 값을 구할 수 없으니 꼭 유의해야 합니다.

이 알고리즘은 쉽게 작성할 수 있다는 장점이 있지만, 3중 반복문을 돌리다보니 $O(V^3)$ 으로 상당히 비효율적이라는 단점이 있습니다. 따라서 정점의 수가 많지 않거나 모든 쌍에 대한 최단거리를 구해야만 할 때 사용하는 것이 좋고, 정점의 수가 많아진다면 필요한 지점들에 대해서만 다익스트라를 돌려서 해결하는 것이 좋습니다.

위의 그래프에 대한 플로이드 워셜 코드는 다음과 같습니다.

```python
import sys

INT_MAX = sys.maxsize

# 변수 선언
# 정점의 수 : 5, 간선의 수 : 8인 그래프
n, m = 5, 8

# dist 초기값을 전부 아주 큰 값으로 설정
dist = [
    [INT_MAX] * (n + 1)
    for _ in range(n + 1)
]

# 자기 자신으로 가는 값은 0으로 설정해줘야 함에 유의합니다.
for i in range(1, n + 1):
    dist[i][i] = 0

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
    dist[x][y] = min(dist[x][y], z)

for k in range(1, n + 1): # 확실하게 거쳐갈 정점을 1번부터 N번까지 순서대로 정의합니다.
    for i in range(1, n + 1): # 고정된 k에 대해 모든 쌍 (i, j)를 살펴봅니다.
        for j in range(1, n + 1):
            # i에서 j로 가는 거리가 k를 경유해 가는 것이 더 좋다면
            # dist[i][j]값을 갱신해줍니다.
            dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

# 모든 쌍에 대한 최단거리 결과를 출력합니다.
for i in range(1, n + 1):
    for j in range(1, n + 1):
        # 불가능한 경우에는 -1을 출력합니다.
        if dist[i][j] == INT_MAX:
            print(-1, end=" ")
        else:
            print(dist[i][j], end=" ")
    print()
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.