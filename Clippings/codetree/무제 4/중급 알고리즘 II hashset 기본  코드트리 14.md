---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-minimum-spanning-tree/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Kruskal

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 크루스칼 알고리즘

N개의 도시가 있는데, 그래프 구조로 되어 있는 길을 모두 건설할 돈이 없어서 최소한의 비용만 투자하여 모든 도시를 어떻게든 이어주려고 합니다. 즉, 다음과 같은 방식으로 길을 선택하려는 것이지요.

![](https://contents.codetree.ai/problems/1914/images/introductions-7db54583-abb0-4774-a037-7dc262ebde41.png)

우리는 최소한의 간선을 사용하여 그래프 내 모든 정점을 이어준다면, 그것을 Spanning Tree라고 부를 것 입니다. 왜 이게 트리냐고요? 놀랍게도 N개의 정점에 N-1개의 간선이 존재하는 그래프는 트리입니다. 실제로 위의 예제 같은 경우도 위치를 약간 바꿔주면 다음과 같이 우리에게 친숙한 트리가 보입니다. 트리는 사이클이 없으며, 모든 노드들이 다 연결되어있다는 특징을 갖고 있습니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-24d51679-6400-42ad-a2ee-9b275b18d852.png)

이것은 가중치가 없을 때의 일이고, 가중치가 있다면 조금 이야기가 달라집니다. 똑같이 N-1개의 간선을 채택하였다 하더라도 상황에 따라 가중치의 합이 다를 수 있으므로, 최소한의 비용을 사용하기 위해선 특정한 경로를 채택해야 할 것입니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-0edf77d5-d320-4790-935f-0df54e89d20d.png)

우리는 가중치가 있을때 최소한의 비용을 사용한 Spanning Tree를 Minimum Spanning Tree라고 부르고, 일반적으로 줄여서 MST라고 부릅니다.

이제 MST를 구하는 알고리즘 중 하나인 크루스컬 알고리즘 (Kruskal Algorithm)에 대해 알아보도록 하겠습니다.

아이디어는 쉽습니다. MST는 가중치의 합을 최소로 하는 Spanning Tree이니, 가중치가 작은 간선부터 고르는 것 입니다.

다음 그래프에서 크루스컬 알고리즘을 생각해보겠습니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-e05c8847-b9b5-4afc-b8f5-16216d5b0a75.png)

먼저 가중치가 가장 작은 1이 적혀있는 간선을 고르게 됩니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-397520b1-3569-4858-bcee-7d7ed26a1a42.png)

순서대로 고르면 됩니다. 다만, 같은 가중치를 갖는 간선이 여러 개인 경우 그 중 아무 간선이나 고르시면 됩니다.

이제 가중치가 5인 간선까지 골라졌다고 생각해보겠습니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-76da5d94-309d-48a8-a767-f53248f956a1.png)

그 다음 가중치가 6인 간선을 고르고자 하는 찰나에, 만약 6인 간선을 고르게 되면 다음과 같이 사이클이 발생하게 됩니다!

![](https://contents.codetree.ai/problems/1914/images/introductions-8f1db3b3-ffeb-4d1a-a2c6-afc9e8e5ec47.png)

노드의 수가 3개라면 당연히 간선이 2개가 되어야 MST가 될텐데, 다음과 같이 사이클이 발생하면 깨지게 됩니다. MST에서 가장 중요한 성질은, 트리이기 때문에 절대 사이클이 생겨서는 안됩니다.

그렇다면 결국 사이클이 발생하지 않도록 해야하는건데, 어떻게 찾아낼 수 있을까요? 답은 바로 앞에서 배웠던 **Union-Find** 입니다.

방법은 간단합니다. 특정 간선을 선택하면, 두 노드에 union 연산을 수행합니다. 그렇게 되면 같은 집합이 될 것입니다. 만약 사이클이 발생하게 된다면, 이미 두 노드는 같은 집합에 속한 상태이니, 미리 체크하여 같은 집합이라면 합치지 않고 넘어가는 겁니다!

위의 경우에서는 가중치가 6인 간선이 골라졌을 경우에 노드 5번과 노드 8번이 같은 루트 노드를 두고 있는지를 판단했어야 합니다. 즉, `find(5)` 와 `find(8)` 가 동일하다면 간선을 추가하면 안된다는 뜻입니다.

이처럼 크루스칼은, 간선의 가중치가 작은 것부터 순서대로 보면서 해당 간선 양 끝에 있는 두 노드 x, y에 대해 find(x), find(y)값을 비교하여 일치하지 않는 경우에만 간선을 선택해주고 union(x, y)를 진행해주는 식으로 계속 진행하면 됩니다.

따라서 가중치가 6인 간선은 선택되지 않고, 그다음 가중치인 7을 보게 되었을 때, find(5)와 find(7) 값은 다르기 때문에 다시 간선을 선택하며 union(5, 7)을 거치게 됩니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-553e0351-335e-4df5-9a88-c68a614384de.png)

이러한 과정을 모든 간선에 대해 진행하면, 그래프에서 노드의 수를 N이라 했을 때 최종적으로 선택된 간선의 수는 N - 1개가 되며, 이 N - 1개의 간선이 결국 MST를 이루게 됩니다.

![](https://contents.codetree.ai/problems/1914/images/introductions-b4aac10a-f2d9-4977-b605-3bb2ecc343c5.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-ce16b752-9f05-4666-9510-6b3b604e9d82.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-74cb9973-0de5-494e-834f-14bf934bfe0d.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-26a8004a-5161-4e1b-b905-a3a7805f7a3b.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-d6c38769-1a5e-4470-bc2a-68a57030126e.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-efaca91b-a42a-47e4-b54f-51ae9274f744.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-6cd9176a-0054-4119-83b2-3c25d25d5e7d.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-7e9d50c3-5ae7-4434-85e3-19d6b3c32315.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-a9efc387-20e6-4cad-a8c2-92f5a3179a4b.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-3c5a396a-01c9-416e-b972-aefb4e871d06.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-14116500-de74-4e32-afcc-34f51a438e0b.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-814a1ce8-1b3d-4ee4-9c67-63ac969a8557.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-5a2a8e36-4d2a-412e-9840-09fc86027305.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-5c644e9e-0347-4cdf-a38f-aea71fdb17e4.png) ![](https://contents.codetree.ai/problems/1914/images/introductions-e81235e9-f4b6-4468-9d89-0f73aefa8384.png)

1 / 15

따라서, Union-Find를 활용하면 크루스컬 알고리즘은 정렬 한 번이면 쉽게 구현할 수 있습니다. 그래프 내 간선의 수를 E라 했을 때, 간선을 정렬하는 데 $O(ElogE)$ 이며, 각 간선에 대해 union-find는 $O(log N)$ 이므로 $ElogE + ElogN$ 가 되어 총 시간복잡도는 $O(ElogE)$ 가 됩니다.

크루스컬 알고리즘 코드는 다음과 같습니다.

```jsx
function kruskal()
    mst = []                       // mst를 담을 배열입니다.
    sort edge[] by length          // 간선을 가중치 기준으로 오름차순 정렬합니다.
    uf = uf_init(|V|)              // uf 배열을 노드의 수 |V|만큼 초기화합니다.

    for E in edge[]                // 각각의 간선에 대해 
        u, v = E                   // 간선을 이루고 있는 두 노드 u, v를 보며
        if find(u) != find(v)      // u, v의 루트 노드가 다른 경우에만
            mst.push(E)            // mst에 해당 간선을 넣어주고
            union(u, v)            // u, v를 같은 루트 노드를 갖도록 만들어줍니다.
    
    return mst
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.