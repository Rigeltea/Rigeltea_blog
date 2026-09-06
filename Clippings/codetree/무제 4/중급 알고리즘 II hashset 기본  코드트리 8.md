---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-adjacent-common-ancestor-nodes/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. LCA

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## LCA

트리 정보가 주어졌을 때 두 정점 a, b의 LCA(Lowest Common Ancestor)는 a와 b의 공통 조상 중 깊이가 가장 깊은 조상을 뜻합니다.

![](https://contents.codetree.ai/problems/1022/images/introductions-27120638-8d35-4d66-9645-062840b68326.png)

예로 위의 그림에서 9번 정점과 4번 정점의 LCA는 6번이 됩니다.

![](https://contents.codetree.ai/problems/1022/images/introductions-31009f5d-8e3e-4977-93a7-1515263822a2.png)

LCA를 구하는 쉬운 방법 중 하나는 주어진 트리에 있는 각 노드의 깊이(depth)를 이용하는 것입니다. 깊이는 처음 주어진 트리에서 DFS 방법으로 순회하며 자식 노드의 깊이를 부모 노드의 깊이 + 1로 값을 갱신해주는 식으로 진행이 가능합니다.

![Image](https://contents.codetree.ai/problem_factory/images/b5e80075-9c99-464f-ab5d-3b8d69cc18f7.webp)

이렇게 각 노드에 대해 깊이를 구해주는 코드는 다음과 같습니다.

```python
# 트리 순회를 진행합니다.
# 동시에 depth를 기록해줍니다.
def dfs(x):
    # 노드 x의 자식들을 살펴봅니다.
    for y in children[x]:
        # depth값을 갱신해주며
        # 재귀적으로 탐색합니다.
        depth[y] = depth[x] + 1

        dfs(y)
```

이제 다음 두 과정을 통해 두 정점 a, b의 LCA를 구해줄 수 있습니다.

(1) Step 1. 두 노드 a, b의 depth를 비교하여 depth가 더 큰 쪽의 노드를 골라 부모를 쭉 따라가며 더 작은쪽 depth로 맞춰줍니다.

위 문제에서는 9번 노드의 높이는 4이고 4번 노드의 높이는 5이기에, 4번 노드를 높이 4에 해당하는 조상인 5번 노드로 변경해줍니다.

![Image](https://contents.codetree.ai/problem_factory/images/4dca8626-0b74-48ac-a5b9-dc86bc945307.webp)

Step 1에 해당하는 코드는 다음과 같습니다.

```python
# Step 1.
# 두 노드 a, b의 depth를 비교하며
# depth가 더 큰 쪽을 위로 올리는 것을 반복하며 두 노드의 depth를 맞춰줍니다.
while depth[a] != depth[b]:
    if depth[a] > depth[b]:
        a = parent[a]
    else:
        b = parent[b]
```

(2) Step 2. 두 노드 a, b가 일치해질때까지 한 칸씩 위로 올라갑니다.

Step 1을 통해 이제 두 노드의 높이가 일치해졌기에, 두 노드는 계속 부모를 따라 한 칸씩 올라가면 됩니다. 그러다 두 노드가 일치하게 되는 경우, 그때의 노드가 LCA가 됩니다.

위의 경우에서 9번 노드와 5번 노드는 한 칸씩 동시에 올라가다 보면 최초로 두 노드가 6이 되었을 때 만나게 됩니다.

![Image](https://contents.codetree.ai/problem_factory/images/0cd1d973-be09-4cbe-8af7-7398eaa8beae.webp) ![Image](https://contents.codetree.ai/problem_factory/images/0d852125-6d21-461c-95ad-e3d8258d0dfb.webp) ![Image](https://contents.codetree.ai/problem_factory/images/67b4d95f-4c7d-48b0-8dda-f47bec19d885.webp)

1 / 6

Step 2에 해당하는 코드는 아래와 같습니다.

```python
# Step 2.
# 두 노드 a, b가 일치해질떄까지
# 한 칸씩 위로 올라갑니다.
while a != b:
    a = parent[a]
    b = parent[b]
```

depth를 구하는데 $O(N)$ 이 소요되며, 이후 a, b에 대한 LCA를 구하기 위해 최대 n개의 노드를 봐야 하므로 총 $O(N)$ 의 시간이 소요됩니다. 즉, $O(N)$ 에 두 노드에 대한 LCA를 구할 수 있습니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.