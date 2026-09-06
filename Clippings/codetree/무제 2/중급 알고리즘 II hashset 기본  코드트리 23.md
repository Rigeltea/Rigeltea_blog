---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-bookshelf-clean/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Doubly-LinkedList

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 연결 리스트의 head, tail 관리하기

연결 리스트의 head와 tail은 각각 가장 앞에 있는 노드와 가장 뒤에 있는 노드를 뜻합니다.

하나의 연결 리스트의 head와 tail을 관리하는 작업은 단순해보이지만 사실 가장 까다롭고 틀리기 쉽습니다.

먼저, 빈 연결 리스트를 생각합시다. head와 tail은 모두 `Null` 노드일 것입니다.

```python
head = None
tail = None
```

이제, "단일 노드 삽입과 노드 삭제"에서 했던 기억을 되살려봅시다.

노드 `u` 는 `head` ~ `tail` 의 연결 리스트에 속해 있고, 단일 노드 `singleton` 은 그렇지 않을 때, `u` 의 뒤에 `singleton` 을 삽입해봅시다.

### Python3 코드

```python
# 노드 u 뒤에 단일 노드 singleton를 삽입
def insert_next(u, singleton):
    global tail

    # singleton의 prev와 next를 설정
    singleton.prev = u
    singleton.next = u.next
    
    # singleton의 이전 노드의 next와
    # 다음 노드의 prev를 설정
    connect(singleton.prev, singleton)
    connect(singleton, singleton.next)
    
    # tail 처리
    if singleton.next is None:
        tail = singleton
```

동영상을 통해 자세한 과정을 알아보세요.

![](https://contents.codetree.ai/problems/3999/images/introductions-1eb930b4-ac52-4eae-a1dd-bfdaa95a9bd9.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-fc25a307-600b-4870-8d7e-1c286f747edd.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-89b97bcf-ea82-4ebf-bf44-23e29dda8705.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-24598d5b-82e5-4ada-b7b5-55581df40d62.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-f0f24c63-3108-471d-a38b-41f8a4b4bef6.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-5d84c6bb-dab8-4bde-a1eb-e59df3d7c899.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-e113bb9e-4bb7-4eb1-8001-1c4e820925fa.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-1336da13-c99e-4a80-ba38-98499222e246.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-95f11fd2-fa3c-422c-a7da-e011b8516c16.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-3c89e033-af92-4c62-9254-264169df47de.png) ![](https://contents.codetree.ai/problems/3999/images/introductions-be3c9e4d-b149-4abc-baa4-3a6fa8a546b9.png)

1 / 11

`tail` 이 바뀌는 케이스를 눈치 채셨나요? 또한, `head` 는 왜 바뀌지 않는지 알아채셨나요?

이중 연결 리스트를 가지고 여러 작업을 수행할 때 `head` 와 `tail` 을 정확하게 관리하기 위해서는, 구현의 작동 과정을 정확하게 이해하고 케이스를 꼼꼼하게 분석해야만 합니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.