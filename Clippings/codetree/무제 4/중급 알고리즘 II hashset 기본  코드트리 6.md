---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-node-best-count/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Tree DP

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 상태 정의와 Tree DP

각 정점에 값이 적혀있는 트리 정보가 아래와 같이 주어졌을 때, 색칠된 노드끼리는 인접하지 않도록 각 노드에 색칠을 적절하게 하여 색칠된 노드에 적혀있는 수들의 합이 최대가 되도록 하려고 합니다.

![](https://contents.codetree.ai/problems/1050/images/introductions-6d830d1f-4c2f-4647-a8ee-d9a5758974c7.png)

위 그림에서는 4번, 7번, 2번 노드를 색칠했을 때 3 + 6 + 10 = 19로 최대 점수를 얻게 됩니다.

![](https://contents.codetree.ai/problems/1050/images/introductions-c84b5643-83dc-4012-927d-e5d0b6b4e58b.png)

이 문제는 어떻게 해결해 볼 수 있을까요?

이 문제를 만약 최대 값인 노드를 우선적으로 골라주는 그리디 방법으로 시도한다면 쉽게 반례를 찾을 수 있기 때문에 불가능합니다.

하지만 관찰을 통해 i번 노드의 자식 번호를 $c_1, c_2, ..., c_k$ 라 했을 때, 이 문제는 다음 특징을 띠고 있다는 것을 알 수 있습니다.

- i번 노드를 색칠하지 않는다면, $c_1, c_2, ..., c_k$ 는 색칠을 하던, 하지 않던 전혀 상관 없습니다.
- i번 노드를 색칠한다면, $c_1, c_2, ..., c_k$ 는 전부 색칠되지 않아야 합니다.

즉, i번 노드를 색칠하는 경우 / 색칠하지 않는 경우에 대해 조사할 때 자식 노드들이 색칠이 되어 있는지 / 없는지에 대한 여부가 중요한 영향을 끼친다는 사실을 알 수 있습니다. 더 나아가서 만약 각 자식 노드의 서브트리에 대해 해당 노드가 색칠이 된 경우 중 얻을 수 있는 최대 점수 / 색칠이 되지 않은 경우 중 얻을 수 있는 최대 점수가 미리 계산이 되어있다면, 현재 i번 노드의 서브트리에 대한 최대 점수를 계산할 수 있다는 사실도 발견할 수 있습니다.

이 관찰을 정리해보자면 `DP[i][j] : i번 노드의 서브트리에서 j = 0이면 정확히 i번 노드를 색칠하지 않은 상황, j = 1이면 정확히 i번 노드를 색칠한 상황이라고 했을 때, 이 상황에서 조건을 만족하며 얻을 수 있는 최대 점수` 라 정의하여 다음 점화식을 세워볼 수 있습니다.

- Case 1. i번 노드에 색칠을 하지 않는 경우 (=DP\[i\]\[0\])
	i번 노드를 색칠하지 않는다면, $c_1, c_2, ..., c_k$ 는 색칠을 하던, 하지 않던 전혀 상관이 없으므로 이 경우에 얻을 수 있는 최대 점수에 대한 식으로 정의됩니다.
$$
DP[i][0] = max(DP[c_1][0], DP[c_1][1]) +  ... + max(DP[c_k][0], DP[c_k][1])
$$
- Case 2. i번 노드에 색칠을 하는 경우 (=DP\[i\]\[1\])
	i번 노드를 색칠한다면, $c_1, c_2, ..., c_k$ 는 전부 색칠되지 않아야만 하므로 이 경우에 얻을 수 있는 최대 점수에 대한 식으로 정의됩니다. 이 경우에는 i번 노드를 색칠하게 되어 추가적으로 얻게되는 점수인 $A[i]$ 를 더해줘야 합니다.
$$
DP[i][1] = DP[c_1][0] +  ... + DP[c_k][0] + A[i]
$$

DP는 큰 문제를 풀기 위해 이미 풀려있는 작은 문제의 답을 이용하는 방식이기에, $DP[i][0], DP[i][1]$ 값을 구하기 위해서는 미리 자식들에 해당하는 DP값이 구해져 있어야만 합니다. 이는 DFS를 통한 트리 탐색과 함께 쉽게 구현이 가능하며, 이를 통해 가장 말단 노드인 리프노드부터 값이 채워지게 됩니다. **즉, 이러한 Tree DP 문제에서의 초기 조건은 리프 노드에 대한 정의로 이루어져 있습니다.**

이 문제에서는 리프 노드 $l$ 의 경우 해당 노드를 색칠하지 않으면 점수를 얻을 수 없으므로 $DP[l][0] = 0$, 색칠하게 되면 정확히 해당 노드에 적혀있는 수 만큼 점수를 얻게 되므로 $DP[l][1] = A[l]$ 이 됩니다. 초기조건이 정해지고 나면 그 위의 노드들은 점화식에 따라 DP 값을 채워주기만 하면 됩니다. 그 과정은 아래와 같습니다.

![](https://contents.codetree.ai/problems/1050/images/introductions-6d63a317-dbcf-414c-9872-4c555c9370f2.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-174434bb-c323-4b9e-aa30-035577d37bf8.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-23eacc61-28f8-40a2-a5d6-a753b7eb9cfc.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-521dd29f-ba00-46e6-aced-63a93a6a9562.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-870f5a2e-e1b9-48ef-b025-69cdbcdbdd66.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-59c59706-123c-4347-984f-ef60f5eb1600.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-2d325149-4749-44cf-b066-46a208ea9eed.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-867fe2a4-6b72-40b3-b24b-85d1058bd771.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-f6c74f7f-3a81-4c77-96c0-eae55b54f3ba.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-52632b3d-82d7-466b-97f1-599dcdee74f8.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-e7dfd0bb-bd17-40dd-94eb-7ace62b6b6a9.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-afcf0ee0-6a3a-45d8-b157-dcfe2469f38e.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-84d1e17c-8d9b-429a-8c64-f5a5da9a1f96.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-1f566332-73bf-4ace-b2bd-0ff60ea5c3fd.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-16d4d84d-9809-49e5-bfa2-052c73682d2c.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-752cc17b-4a07-4ec6-b8a3-ad35daa7ddcc.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-b52ae623-251b-4aef-8e34-a2b6d9dc22f4.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-e9f7c781-f13f-46da-bd0f-feb6eb25095b.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-dbe52c46-6216-4e64-b564-cb0fdf92b167.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-d94b5bf1-33b9-413f-908d-d379461e382f.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-34f4d1f3-c79c-486d-913d-e4d434dd67d3.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-36868e12-3b54-4b81-9209-e2541147d66d.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-b9f8e913-7ff5-400d-9b1b-e68daa66bfc9.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-883e020f-d10c-40e0-a071-43b62bd9c851.png) ![](https://contents.codetree.ai/problems/1050/images/introductions-694b8f62-b939-40f6-8054-7cc9a433b70d.png)

1 / 25

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.