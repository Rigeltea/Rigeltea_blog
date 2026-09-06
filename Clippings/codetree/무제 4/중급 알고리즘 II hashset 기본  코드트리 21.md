---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-height-of-friends-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Topological Sort

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 위상정렬과 사이클

다음과 같이 사이클을 이루고 있는 경우 순서를 정의할 수 없기 때문에 위상정렬을 적용할 수 없다고 했습니다.

![Image](https://contents.codetree.ai/problem_factory/images/1ba1fb42-4323-46f5-bfe1-8aba404156a0.webp)

사이클이 없는 방향성 그래프에서는 항상 위상정렬이 가능하고, 사이클이 있는 방향성 그래프에서는 항상 위상정렬이 불가합니다. **즉, 주어진 방향성 그래프에 사이클이 있는지를 판단하기 위해서는 dfs, in-degree 등의 방법으로 위상정렬을 시도해본 뒤 위상정렬이 불가하다면 사이클이 존재한다고 판단하면 됩니다.**

위상정렬이 불가능했다는 건 어떻게 쉽게 판단할 수 있을까요?

간단합니다. in-degree 방법을 사용하여 위상정렬을 시도해본 뒤, queue에 들어간 노드의 수가 그래프에서 주어진 노드의 수와 일치하는지를 확인하면 됩니다. 사이클이 있다면 모든 노드의 in-degree가 0이 될 수가 없기에 queue에 모든 노드가 들어갈 수가 없습니다. 따라서 이를 이용하여 방향성 그래프에 사이클이 있는지를 $O(V+E)$ 에 판단할 수 있습니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.