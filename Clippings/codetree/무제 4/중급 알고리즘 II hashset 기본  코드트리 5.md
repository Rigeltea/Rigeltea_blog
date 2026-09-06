---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-calculating-an-integer-for-a-node/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Tree DP

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Tree DP

각 정점에 값이 적혀있는 트리 정보가 아래와 같이 주어졌을 때, 각각의 노드마다 자신을 포함하여 자손 노드들에 적혀있는 수들의 합을 구해보려고 합니다.

![](https://contents.codetree.ai/problems/1049/images/introductions-2c869286-bef6-41b1-83ee-f72ec1461dfd.png)

위 그림에서 예를 들어 6번 노드의 경우 자신을 포함한 자손 노드 번호가 6, 2, 3, 5 이므로 각 노드에 적혀있는 수들의 합인 2 + 3 + 3 + 4 = 12가 나와야 합니다. 즉, 우리가 얻고 싶은 결과는 아래와 같습니다.

![](https://contents.codetree.ai/problems/1049/images/introductions-8be77b21-2a6c-4cfe-9faf-26b2eab72b68.png)

이를 각 노드를 정한 뒤 해당 노드에서 자식 노드로 움직이는 것을 재귀적으로 반복하는 탐색을 진행하는 완전탐색 방법을 통해 구현한다면, 각 노드를 정하는데 $O(N)$, 각 노드마다 최대 확인해야 하는 노드 수가 $O(N)$ 이 되어 총 $O(N^2)$ 의 시간복잡도를 갖게 됩니다.

이는 DP를 활용하여 $O(N)$ 의 시간복잡도로 만들 수 있습니다. 아직 동적계획법에 대해 잘 모르신다면 [DP](https://www.codetree.ai/missions/2/problems/fibonacci-number/introduction) 유형을 공부하시고 나서 다시 이 설명을 읽는 것을 추천드립니다.

`DP[i] : i번 노드를 루트로 하는 서브 트리에 있는 노드에 적힌 수들의 합` 으로 정의했을 때, 각 DP값은 문제에서 원하는 그 값이 됩니다. i번 노드의 자식 번호를 $c_1, c_2, ..., c_k$ 라 했을 때, 다음 점화식을 만족하게 됩니다. 정의상 모든 자식의 DP값에 현재 노드에 적혀있는 수인 $A[i]$ 를 더하면 서브 트리에 있는 노드에 적힌 모든 수의 합이 구해지기 때문입니다.

$$
DP[i] = DP[c_1]+DP[c_2]+...+DP[c_k]+A[i]
$$

DP는 큰 문제를 풀기 위해 이미 풀려있는 작은 문제의 답을 이용하는 방식이기에, $DP[i]$ 값을 구하기 위해서는 미리 자식들에 해당하는 DP값이 구해져 있어야만 합니다.

이는 DFS를 통한 트리 탐색과 함께 쉽게 구현이 가능합니다. 트리에서의 DFS는 깊이우선탐색 특성상 **모든 자손을 방문한 이후에 다시 현재 노드의 위치로 되돌아오게 됩니다.** 이를 이용하면 됩니다. 아래와 같이 현재 노드 x를 기준으로 먼저 DFS 탐색을 전부 진행한 뒤, **퇴각하기 직전에 DP 값을 갱신해주는 식으로 값을 계산해주면 됩니다.**

![](https://contents.codetree.ai/problems/1049/images/introductions-e4b8bbfd-781e-4147-920c-79a66531e56a.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-1ac3e727-40e9-439d-8685-a9461994ea9b.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-ed687348-5986-4b32-8c29-229c933b5dde.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-1b827aef-6181-49fb-a7f4-291771bf3ab8.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-d37eea01-cbc8-4ea8-a1c6-4c387794e9e8.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-85a9af21-0cb4-465b-826d-256332d51d66.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-206c2a60-ed79-4439-9bb3-10e73157c432.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-e9fb9470-ed23-435e-8397-98ab5ed86e0f.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-03c95151-b6fe-4d87-94a1-e5b5195a2a13.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-80561edf-dea1-40fa-89ff-f5c5c5a2ce4b.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-51c8d783-00f2-4d36-a4e8-cee04fa4465f.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-93210076-f7eb-404e-9936-8d0e77d96e08.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-13edbed5-62a5-4011-82aa-1e5691b1c3c4.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-31b04812-8a48-4cc7-b9f7-ba85d588808d.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-8c103dbf-3c8a-4a7a-86b0-879dff763581.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-6814c104-c0e2-44ed-a69a-acb0df48a96f.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-819aefa2-22b9-462e-8266-06f77880635b.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-ec6deda5-f018-4b62-929d-d1235b71ad8a.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-e5d694e6-5635-473f-931e-d417890ef3cf.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-c589f69f-64ba-4140-ba6c-8bdaf044a3e5.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-72464ac4-e1a2-40ec-91b5-f00dd76c7949.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-9e92db82-9e16-45b6-87fd-67fd3d4a7b07.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-f7120917-1b8f-4e7d-97fb-fea6fbd3c529.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-2c4bec57-d0d1-49ae-83b8-e0190e08b059.png) ![](https://contents.codetree.ai/problems/1049/images/introductions-c4524d95-7070-48da-9bc7-631ab2ba6db5.png)

1 / 25

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.