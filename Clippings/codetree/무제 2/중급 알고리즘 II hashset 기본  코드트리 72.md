---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-longest-student-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 모든 점으로 부터 특정 점까지의 최단거리

다익스트라 알고리즘 (Dijkstra Algorithm)은 **특정 시작점** 에서 **다른 모든 정점** 으로 가는 최단거리를 각각 구해주는 알고리즘이라 했습니다. 그렇다면 반대로 **모든 정점** 으로부터 **특정 도착점** 까지의 최단거리는 어떻게 구해볼 수 있을까요?

예를 들어 다음 그래프에서 각 정점(1~4)으로부터 5번 정점까지의 최단거리를 각각 구해보고 싶은 것입니다.

![](https://contents.codetree.ai/problems/2235/images/introductions-3a05d4bb-c502-4778-8e92-7b6b33aa8185.png)

가장 naive한 방법은 각 정점에 대해 다익스트라 알고리즘을 각각 적용하여 최단거리를 구해보는 것입니다. 정점의 수를 V라 했을 때 다익스트라 알고리즘의 시간복잡도는 $O(|E|log|V|)$ 이므로 이 방법의 시간복잡도는 $O(|V||E|log|V|)$ 가 됩니다.

하지만 이렇게 생각해보는건 어떨까요?

> 그래프의 모든 간선을 뒤집은 뒤, 5번 정점에서 다른 모든 정점까지 가는 최단거리를 구하면 문제에서 원하는 답이 된다.

![](https://contents.codetree.ai/problems/2235/images/introductions-8a8665cb-7da2-4d6b-a5ec-fdfea15719cb.png)

따라서 다른 모든 정점으로부터 특정 지점까지의 최단거리를 전부 구해야 하는 경우에는 간선을 뒤집어 다익스트라 알고리즘을 한번 적용하면 되므로 시간복잡도 $O(|E|log|V|)$ 에 해결이 가능합니다. 단, 양방향 그래프의 경우 의미상 굳이 뒤집어주지 않아도 됨에 유의합니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.