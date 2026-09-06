---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-common-ancestor-of-node-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. LCA

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## LCA와 Sparse Table

트리 정보가 주어졌을 때 두 정점 a, b의 LCA(Lowest Common Ancestor)는 a와 b의 조상 중 깊이가 가장 깊은 조상을 뜻한다고 했습니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-5c682f03-7bdd-4161-abb7-eba2016decd9.png)

두 정점 a, b에 대해 depth를 동일하게 맞춰주고, 두 노드가 일치하기 전까지 한 칸씩 위로 올라가는 방식으로 $O(N)$ 의 시간에 LCA를 찾을 수 있었습니다.

이때 Sparse Table를 사용하면 LCA를 찾는 시간을 $O(logN)$ 으로 줄일 수 있습니다.  
이는 `parent[h][i] = i번 노드에서 2^h번 부모를 따라 위로 올라갔을 때의 노드 번호를 관리` 형태의 2차원 배열을 이용하는 방법입니다.

parent값을 채우는 것은 마치 동적계획법에서의 과정과 같습니다. 초기조건의 경우 `parent[0][i]` 를 채우는 것으로 이는 i번 노드에서 1번(= $2^0$)번 부모를 따라 위로 올라갔을 때의 노드, 즉 바로 부모 노드의 번호를 적어주는 것을 뜻합니다. 따라서 이 과정은 DFS를 통해 트리를 순회하며 계산이 가능합니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-4b6e2365-b620-4e0e-bde8-9e2a3d5f43f1.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-351c05aa-80d4-4fae-b692-d7fc8bd43ec9.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-6d5a34b8-1518-462a-acc5-d41fc4965a92.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-17ba8f70-862f-4742-ac01-c27eb2bb34fd.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-c56f31a6-f0cf-43dd-ab5f-6dad2a604313.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-46f9da03-9446-4d8e-9cd7-aa5c18616adc.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-7cdbab6f-4d9b-4c19-a082-b370ba4f44e3.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-e29e64b8-c3ae-4ca2-9d5b-1c53fbd4c190.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-aefb2663-9030-43a4-9351-29eab9257fd6.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-4defe118-2fbc-4245-8c09-a3e219f7fd8c.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-563ad20b-efb0-402f-8038-ab07d13ddd14.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-0d151491-a629-4f00-afc0-bc0c338b3870.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-3161c642-93a5-4d32-8735-741c21a5ecad.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-e9a65253-b42b-492d-973b-03571a8aca8f.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-ce75d7e2-760f-43ea-a616-bdb50ccd8c91.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-677d1bdc-8d87-4e18-aea1-3d7ed82ceac1.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-52193220-7432-459c-9b89-12c954b23812.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-81ddbf77-d76c-4433-9cfc-686b8cbe6215.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-29ba9d66-dc06-4e66-ba52-fe82fff559bf.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-ebbe05c8-657a-4d70-a2e2-de0a1d1fc885.png)

1 / 20

DFS 탐색과 함께 초기조건을 채워주는 코드는 다음과 같습니다.

```python
# 트리 순회를 진행합니다.
# 동시에 depth를 기록해줍니다.
def dfs(x):
    # 노드 x의 자식들을 살펴봅니다.
    for y in children[x]:
        # depth값을 갱신해주며
        # 재귀적으로 탐색합니다.
        depth[y] = depth[x] + 1

        # 이때 y번 노드에서 1번(=2^0)번 부모를 따라 위로 올라갔을 때의 
        # 노드 번호는 x가 됩니다.
        parent[0][y] = x

        dfs(y)
```

이후 0 ~ h - 1까지는 이미 계산이 되어 있다는 전제 하에 정점 i로부터 $2^h$ 번 위로 올라갔을 때의 위치는 정점 i로부터 $2^{h-1}$ 번 위로 올라간 뒤, 다시 그 노드로부터 $2^{h-1}$ 번 위로 다시 올라가면 바로 구해질 수 있다는 논리를 이용하면 다음과 같은 점화식이 도출됩니다.

$$
parent[h][i] = parent[h - 1][parent[h - 1][i]]
$$

이 내용을 그림으로 나타내면 다음과 같습니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-01d66865-3a45-4b99-a123-c37a03f9325d.png)

이 점화식을 이용하면 $O(NlogN)$ 에 $parent[h][i]$ 값을 전부 구해줄 수 있습니다. 그 까닭은 결국 $2^h$ 번 위로 올라갔을 때의 위치를 구해야 하는 것이므로, 최대로 구해야 하는 h값이 $⌊log{N}⌋$ 이 되기 때문입니다. 따라서 logN \* N 크기의 테이블에 값을 채워야 하므로 시간복잡도는 $O(NlogN)$ 이 됩니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-8b67069a-9338-4fcf-b9c1-aaa19356a814.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-6619e30c-29d6-4cb5-bf6d-32c9e5aad685.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-3ab93d20-2355-45d8-8098-b3dd58b12ec7.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-76ad9712-9b64-4902-9669-7e5eac67d5dd.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-d1f95140-cff5-4ef0-a3ca-90e83c802cfc.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-9f4b32d4-e4e1-4ac3-a953-d0033faa8801.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-9dfdc615-aaa4-4df8-a880-0b1fa87886c6.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-f6079734-2f57-4629-a7a4-8b6a1c11bb03.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-c7bfafca-bc5a-4864-8f06-868f6526413f.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-4bd0692f-f97c-4bff-8476-cd3ceb8fa2e2.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-e8734954-e218-4efa-aed9-f398a07e4f1d.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-08263e6e-1c14-43e4-99a5-ea3c0cc1f4b9.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-9b26089a-a122-455d-a450-fa27d622f549.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-93796920-0edd-4ca9-a725-19b8ed1ce3be.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-d5c18949-3ccf-4c14-9c39-f7ee92b9292f.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-26568e68-4878-4df9-a42e-b26c52337548.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-28f5ed24-8cf9-4a32-8e32-bc69f004095d.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-eca33cac-8b04-420e-8615-3a6fc1777335.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-301484f5-00fb-4988-9800-b747391ac461.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-013a8276-c6db-446b-9a7c-668369c06905.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-e30c9ef4-1516-4b05-a882-2df95d4f9f0e.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-b097e82f-f8a5-4077-88e5-212d5c5e2d8d.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-a57c4a79-b0e9-475e-8061-9793acf30cf6.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-df43a385-8e2a-4988-b38a-5c562f415660.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-471c9cd5-2d53-41d4-b1bd-a522c9d7adf3.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-9fddf438-5fd9-4516-8d10-acc638f3eedb.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-f64bf2a6-5577-440f-a3d9-fcdbaf021391.png)

1 / 27

이렇게 점화식에 따라 parent 값을 완성시키는 코드는 다음과 같습니다.

```python
# parent값을 갱신해줍니다.
for h in range(1, MAX_H + 1):
    # 0 ~ h - 1까지는 이미 계산이 되어 있다는 전제 하에
    # 정점 i로부터 2^h번 위로 올라갔을 때의 위치는
    # 정점 i로부터 2^(h-1)번 위로 올라간 뒤, 
    # 다시 그 노드로부터 2^(h-1)번 위로 다시 올라가면 
    # O(1)에 바로 구해집니다.
    for i in range(1, n + 1):
        parent[h][i] = parent[h - 1][parent[h - 1][i]]
```

이제 다음 두 과정을 통해 두 정점 a, b의 LCA를 구해줄 수 있습니다.

(1) Step 1. 두 노드 a, b의 depth를 비교하여 depth가 더 큰 쪽의 노드를 골라 부모를 쭉 따라가며 더 작은쪽 depth로 맞춰줍니다. 이때 십진수를 이진수로 빠르게 바꾸는 방법 중 하나인 2의 거듭제곱 중 가장 큰 값을 계속 빼주는 원리를 이용합니다.

예를 들어 노드 a에서 높이 13만큼 올라가야 하는 상이라면, 13 = 8 + 4 + 1임을 이용합니다. 노드 a에서 높이 8만큼 올라갔을 때의 노드는 `parent[3][a]` 로 바로 구할 수 있고 이를 a'이라 했을 때 다시 a'에서 높이 4만큼 올라갔을 때의 노드는 `parent[2][a']` 로 바로 구할 수 있고 이를 다시 a''이라 했을 때 마찬가지 방법으로 다시 a''에서 높이 1만큼 올라갔을 때의 노드는 `parent[0][a'']` 으로 바로 구할 수 있습니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-afca5ae8-2b35-48a6-999f-f500538ea47b.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-a96526af-ddab-4e1d-a687-c654a0b4e9cf.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-6db5411b-432e-4d2c-8107-e06a96068985.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-21e3ff51-c696-428b-b173-b513c2cf3fe0.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-a236ed25-5258-46f1-a625-b6a1d4fc53f8.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-4c38df0f-0979-4c1b-a0b1-bafb09ba1a65.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-a7f5093c-1c20-4f62-b139-423039a7a3fb.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-4406ebae-ea66-46e3-b88c-e7c12133a705.png)

1 / 8

13이 8, 4, 1의 합으로 나타내진다는 것은, 해당 수보다 같거나 작은 2의 거듭제곱 수 중 최댓값을 계속 찾아주는 것으로 쉽게 계산이 가능합니다. 13을 넘지 않으면서 가장 큰 2의 거듭제곱 수는 8이며, 남은 5에 대해서는 4가 되고, 남은 1에 대해서는 1이 되기에 이러한 과정을 거쳐 13 = 8 + 4 + 1이 됨을 알 수 있습니다.

즉, $2^{⌊log{N}⌋}$ 에서 시작하여 $2^0$ 까지 순서대로 보며 아직 그만큼 더 위로 올라가야 한다면 parent 를 이용해 노드를 위로 올려주는 식으로 코드를 작성하면 $O(logN)$ 에 두 노드 a, b의 높이를 맞추는 것이 가능해집니다. 이때 2의 거듭제곱승을 $O(1)$ 에 구하기 위해서는 shift (`<<`) 연산을 이용할 수 있으며, (1 << h)로 부터 $2^h$ 값을 바로 얻어낼 수 있습니다.

Step 1 과정에 대한 코드는 다음과 같습니다. 편의상 노드 a를 위로 올려줘야 하는 경우라고 가정한 코드입니다.

```python
# Step 1.
# 노드 a의 높이를 노드 b의 높이까지 끌어올려줍니다.
# 이는 십진수를 이진수로 빠르게 바꾸는 방법 중 하나인
# 2의 거듭제곱 중 가장 큰 값을 계속 빼주는 원리를 이용합니다.
for h in range(MAX_H, -1, -1):
    # a의 높이를 b에 맞추기 위해
    # 아직 2^h 만큼 더 끌어 올려줘도 된다면
    # 그만큼 올라갔을 때의 조상 값으로 변경해줍니다.
    if depth[a] - depth[b] >= (1 << h):
        a = parent[h][a]
```

(2) Step 2. 두 노드 a, b가 일치해질때까지 최대한 위로 올라갑니다.

Step 1을 통해 이제 두 노드의 높이가 일치해졌을 것입니다. 두 노드 a, b 값이 이미 일치한다면 그대로 답이 되겠지만, 그렇지 않다면 두 노드는 계속 부모를 따라 올라가며 일치하게 되는 순간을 구해야 합니다. 이 경우를 그대로 한 칸씩 올라가는 식으로 구현하면 $O(N)$ 의 시간이 소요되겠지만, 약간의 트릭과 함께 parent를 활용하면 이 시간을 $O(logN)$ 으로 줄일 수 있습니다.

아이디어는 실제 두 노드가 LCA를 찾기 위해 추가로 올라가야 하는 높이를 k라 했을 때, 정확히 k - 1까지만 위로 빠르게 올려보내자는 것입니다.

예를 들어 아래와 같이 높이가 동일한 두 노드 a, b가 만나기 위해서는 높이 14만큼 올라와야 하는 상황이라고 생각해봅시다.

![](https://contents.codetree.ai/problems/1044/images/introductions-bfa4fdfb-13a8-4998-8b28-239c55590807.png)

그렇다면 현재 위치에서 13만큼 올라와도 두 노드의 번호는 일치하지 않게 될 것입니다. 이를 이용하면 Step 1과 유사한 방법으로 쉽게 해결이 가능합니다. 두 노드에서 출발하여 Step1과 마찬가지 방식으로 $2^{⌊log{N}⌋}$ 에서 시작하여 $2^0$ 까지 순서대로 보며 아직 그만큼 더 위로 올라가도 a와 b의 값이 다르다면 계속 올라가야만 한다는 뜻이므로 올라가는 것을 반복하면 됩니다. 즉 현재 노드에서 $2^h$ 칸을 올라간 정점 번호인 $parent[h][a]$, $parent[h][b]$ 의 값이 서로 다르다면 parent를 이용하여 $2^h$ 만큼 올라가는 것을 계속 반복하면 됩니다.

![](https://contents.codetree.ai/problems/1044/images/introductions-0ed442b6-5c42-4ff3-8312-8036e16bc906.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-d6401f20-bf34-471c-9a40-46f84a639f2a.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-d76f7314-f983-4cdf-ab75-ef62f9ef1005.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-bb2b30da-295b-4fdb-a311-6acd8b4a641f.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-b0edae69-aaf2-4624-81cf-81a2ca3376a1.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-e4d5c369-63bf-4052-8342-4c3df06fd81b.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-cbd6592a-ac98-46ef-b389-fc57e3e8a694.png) ![](https://contents.codetree.ai/problems/1044/images/introductions-053105ea-57a0-49ef-b057-e616ab661802.png)

1 / 8

**이 과정이 끝났을 때의 a, b값은 LCA 도달 직전인 상황이므로, 최종적인 답은 a의 부모에 해당하는 parent\[0\]\[a\]가 됨에 유의합니다.**

Step 2 과정에 해당하는 코드는 다음과 같습니다.

```python
# Step 2.
# 두 노드 a, b가 일치해지기 직전까지
# 위로 올라갑니다.
# 이때 역시 해당 높이에 도달하기 위해 점프해야 하는 값을 x라 한다면
# x라는 십진수를 이진수로 빠르게 바꾸는 방법 중 하나인
# 2의 거듭제곱 중 가장 큰 값을 계속 빼주는 원리를 이용합니다.
# 단, 그 시점을 찾기 위해
# 두 노드가 일치해지기 바로 직전까지 최대한 올라가는 방법으로 진행합니다.
for h in range(MAX_H, -1, -1):
    if parent[h][a] != parent[h][b]:
        a = parent[h][a]
        b = parent[h][b]

# 이제 a, b는
# 같아지기 바로 직전의 위치까지 올라온 것이므로
# 최종 답은 a의 부모가 됩니다.
lca = parent[0][a]
```

이렇게 parent라는 Sparse Table을 이용하게 되면 처음 parent 값을 준비하는데에는 $O(NlogN)$ 의 시간이 소요되지만 이후 LCA를 찾는 데에는 $O(logN)$ 의 시간이 소요됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.