---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-diameter-of-tree/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. 트리

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 트리의 지름

트리에서는 어떠한 두 정점을 고르더라도 두 정점 사이를 연결하는 경로는 유일하게 결정된다는 특징이 있습니다. 각 간선에 가중치가 있는 트리 정보가 주어졌을 때, 모든 정점 쌍에 대한 거리 중 가장 긴 경로의 길이를 트리의 지름이라고 부릅니다.

아래 그림에서 트리의 지름은 $6+6+2+4=18$ 이 됩니다.

![Image](https://contents.codetree.ai/problem_factory/images/9127d3a8-22c6-4d9b-924e-6e3661ed2695.webp)

트리의 지름을 가장 쉽게 구하는 방법은 다음과 같습니다.

1. 아무 정점을 시작점으로 정하고, DFS를 이용해 시작점으로부터 가장 먼 정점을 구합니다. 거리가 동일한 정점이 여러 개라면 아무 정점이나 골라도 괜찮습니다. 이렇게 골라진 가장 먼 정점을 $x$ 라 하겠습니다.
2. DFS를 이용해 동일한 방식으로 $x$ 를 시작점으로 하였을 때 가장 먼 정점을 구합니다. 이때 구해진 거리가 지름이 됩니다.

예로 아래 그림에서의 지름을 구해보겠습니다.

![](https://contents.codetree.ai/problems/1040/images/introductions-76ee60c7-66da-4478-8cb0-225b815525ed.png)

1번 정점을 시작으로 가장 먼 정점을 구합니다. 가장 먼 정점은 7번 정점이 됩니다.

![](https://contents.codetree.ai/problems/1040/images/introductions-408ad9b5-a389-4e98-b85d-ac172ef50155.png)

이제 7번 정점을 시작으로 가장 먼 정점을 구합니다. 가장 먼 정점은 5가 되며, 따라서 7번 정점과 5번 정점으로 이루어져 있는 경로의 길이가 트리의 지름이 됩니다.

![Image](https://contents.codetree.ai/problem_factory/images/9127d3a8-22c6-4d9b-924e-6e3661ed2695.webp)

따라서 트리의 지름을 구하는 데 걸리는 시간은 $O(N)$ 이 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.