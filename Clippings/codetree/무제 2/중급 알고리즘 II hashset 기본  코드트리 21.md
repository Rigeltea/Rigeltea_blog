---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-linked-list2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Doubly-LinkedList

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## ID가 있는 노드 관리하기

각 노드가 고유한 ID를 가질 때에 특정 ID를 갖는 노드를 빠르게 찾아야 할 때가 있습니다.

일반적으로 다음 두 가지 방법으로 노드들을 관리합니다.

## 배열 사용하기

노드의 ID가 0 이상 `MAX_N` 미만이라면, 길이 `MAX_N` 의 배열로 노드들을 관리할 수 있습니다.

### Python3 코드

```python
# 노드를 담고 있는 배열. 초기값은 nullptr입니다.
nodes = [None] * MAX_N

# ID가 42인 노드의 값을 15로 변경
new_node: Node = Node(7)
nodes[42] = new_node

# ID가 42인 노드의 값을 15로 변경
node_id_42: Node = nodes[42]
node_id_42.data = 15

# 이 경우, 포인터의 성질에 의해, 배열에 다시 노드를 대입하지 않아도 됩니다. 
""" nodes[42] = node_id_42 """
```

## HashMap 사용하기

하지만, 만약 이 ID가 10억이 넘어가는 엄청나게 큰 수라면 어떻게 될까요? 길이 10억짜리 배열을 만들려면 아주 많은 메모리가 필요할 것입니다.

이를 해결하기 위해서는 앞에서 배웠던 [HashMap](https://www.codetree.ai/missions/8/problems/hashmap-basic/introduction) 을 이용하여 노드들을 관리해야 합니다. HashMap이란, 해싱을 기반으로 데이터를 관리하는 자료구조입니다. HashMap은 (key, value) 쌍 형태로 데이터를 관리하며, key와 그 key에 따른 value 값을 동시에 저장합니다.

### Python3 코드

```python
# 노드를 담고 있는 HashMap.
nodes = dict()

# ID가 1000000002인 노드
node_with_id_bigId = nodes[1000000002]
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.