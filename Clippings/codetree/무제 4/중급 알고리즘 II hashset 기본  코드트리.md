---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-parent-node-of-the-tree/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. 트리

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 트리의 개념, 용어, 탐색

회사 조직도나, 가계도 같은 것을 보면 대부분 다음과 같은 구조로 되어 있을 것 입니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-69572e23-d283-4fac-b9ab-c1bc003bddca.png)

우리는 이런 구조를 일반적으로 트리 구조라고 합니다. 나무 같지 않다고요? 나무를 180도 돌려서 보면 맨 위에는 큰 하나의 기둥이 있고, 아래로 내려갈수록 가지가 계속 뻗어나오는 것을 볼 수 있습니다. 그렇기 때문에 우리는 이 구조를 트리 구조라고 부르는 것이지요.

트리는 두 지점의 연결 관계로 구성되어 있는데, 계층관계가 존재한다는 것이 특징입니다. 우리는 하나의 연결 관계에서 위쪽에 있는 점을 **부모** 라고 부르며, 아래쪽에 있는 점을 **자식** 이라고 부를 것 입니다.

이 외에도 추가적인 용어들이 많은데, 아래쪽 사진을 참고하면서 용어를 이해해봅시다.

- **노드**: 각 지점을 의미합니다. 정점이라 부르기도 합니다.
- **간선**: 두 노드를 연결하는 선을 의미합니다. 에지라고 부르기도 합니다.
- **루트 노드**: 트리에서 맨 꼭대기를 의미합니다. 위쪽 조직도를 보면, 루트 노드는 회사 대표가 되겠죠?
- **부모, 자식**: 트리에서 연결된 두 노드의 관계를 의미하는데, 더 위쪽에 있는 노드를 부모 노드, 아래쪽에 있는 노드를 자식 노드라고 부릅니다.
- **차수**: 특정 노드를 기준으로, 자식의 수가 얼마나 되는지 의미합니다.
- **깊이**: 루트 노드와 얼마나 떨어져 있는지를 가리키는 말입니다.
- **높이**: 트리에서 깊이가 가장 깊은 노드의 깊이 혹은 1을 더한 값을 의미합니다. 코드트리에서는 앞으로 트리의 높이를 최대 깊이에 1을 더한 값으로 생각하도록 합시다.
- **리프 노드**: 자식을 갖고 있지 않은 노드를 의미합니다.

![Image](https://contents.codetree.ai/problem_factory/images/9f7ba289-f445-46ce-bdd2-b320e76f84b0.webp)

놀랍게도 다음과 같이 부모 자식 관계가 정의되지 않는 경우에도 트리라고 부릅니다. 즉, **트리의 원래 정의는 노드끼리 전부 연결되어 있으면서 사이클이 존재하지 않는 그래프** 입니다. 이런 경우를 **Unrooted tree** 라고 부릅니다. 위의 경우에서 처럼 루트 노드가 설정되어있는 트리는 **Rooted tree** 라고 부릅니다. 참고로 Unrooted tree에서의 차수는 노드에 연결된 간선의 개수이고, 리프 노드의 정의는 차수가 1인 노드가 됩니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-f1b681aa-6d4e-49ac-a11f-04f05c0d4de3.png)

다음 두 예시의 경우, 왼쪽 그림은 모두 이어져 있지 않으므로 트리가 아니며 오른쪽 그림에서는 사이클이 존재하므로 트리가 아니게 됩니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-59d39d22-0f16-4364-9513-453a0712257d.png)

Unrooted tree에서의 **루트 노드는 사람이 정하기 나름입니다.** 트리의 루트 노드가 정해지면 그때부터 부모, 자식, 차수 등이 정의가 되는 것입니다. 다음과 같이 동일한 트리에 대해 1번을 루트로 그릴 수도 있고, 2번을 루트로 그릴 수도 있습니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-8366c9aa-cb18-4242-8873-0116061e6b18.png)

이제 Rooted tree라는 가정 하에서 아래 그림에 대해 트리 탐색을 진행해보도록 하겠습니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-cd0f7454-929b-419e-8ced-ecf21d0e6c40.png)

일반적으로 트리에 대한 정보는 마치 그래프와 같이 두 정점간의 연결 관계만 주어지기 때문에 연결된 두 정점 중 누가 부모이고 자식인지를 알 수가 없습니다. **따라서 양방향 그래프에서 루트 노드를 시작으로 하는 DFS 탐색을 진행하며 이 과정속에서 부모-자식 관계를 정의해 줄 수 있습니다.**

위 그림에서 루트 노드인 1번 정점을 시작으로 DFS를 진행하며 정점 x에서 정점 y로 진입하게 될 즉시 **y의 부모 노드는 x** 라는 정보를 얻어낼 수 있습니다.

![](https://contents.codetree.ai/problems/1013/images/introductions-85ec6e70-c0e7-4e71-89d7-c4ccf7b4b74b.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-62e80e66-6423-4b91-ae58-ec915ec016d5.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-1cb36294-bace-4898-b455-8859331d9fac.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-ddcf4415-924b-4f1b-bc8e-7e0f70829c59.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-d5f78064-b7e8-4d34-9c1b-85292d19dc32.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-706b36c2-9ec6-48f8-afa6-011fd77ea76c.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-45a9a224-9416-43ff-b28e-583ff5490446.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-769376a1-99bf-45dd-8405-53fa35676eb9.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-9f92af3b-21c7-4428-8f0e-d133f6dc7e85.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-4dacd60f-96d8-48bc-97e1-ab352fb049e4.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-f5824424-10de-4734-aee2-cb32d68a09fd.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-8fe99074-023d-43d2-a22d-7526c8ef3bc6.png) ![](https://contents.codetree.ai/problems/1013/images/introductions-b47dc59e-030b-48b2-a725-5e5459deba09.png)

1 / 13

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.