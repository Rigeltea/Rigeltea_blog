---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-size-comparison-3/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Topological Sort

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 사전순으로 가장 앞선 위상정렬

아래 그래프에서는 다양한 위상정렬이 가능합니다.

![](https://contents.codetree.ai/problems/1880/images/introductions-da0bf8aa-4bfb-49d6-9d01-96ee780134f9.png)

`1 -> 3 -> 6 -> 2 -> 5 -> 7 -> 4`, `1 -> 4 -> 3 -> 6 -> 2 -> 5 -> 7` 등 여러 위상정렬이 가능하지만, 사전순으로 가장 앞선 답은 `1 -> 3 -> 4 -> 6 -> 2 -> 5 -> 7` 이 됩니다.

사전순으로 가장 앞선 답을 구하는 것은 생각보다 간단합니다. **in-degree를 이용한 위상정렬 방법을 쓰되, 큐 대신 번호가 가장 작은 노드를 먼저 골라주는 우선순위 큐를 이용하면 됩니다.** 우선순위 큐를 이용하면 in-degree가 0인 노드 중 번호가 가장 작은 노드를 우선적으로 골라줄 수 있기에 사전순으로 앞선 결과를 얻을 수 있습니다. 이 방법을 사용하면 우선순위 큐에 정확히 V개의 노드가 들어오게 되므로 시간복잡도는 $O(VlogV+E)$ 가 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.