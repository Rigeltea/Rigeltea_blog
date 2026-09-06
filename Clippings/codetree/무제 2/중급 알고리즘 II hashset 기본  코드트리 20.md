---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-linked-list1/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Doubly-LinkedList

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 단일 노드 삽입과 노드 삭제

Novice High에서 [이중 연결 리스트](https://www.codetree.ai/missions/6/problems/singly-and-doubly/introduction) 에 대해서 배웠습니다.

![](https://contents.codetree.ai/problems/3996/images/introductions-c3748a6e-c9bd-48e5-a2e7-dedf4f64ba6e.png)

이중 연결 리스트란, 탐색은 $O(N)$ 의 시간이 걸리지만, 삭제와 삽입에는 $O(1)$ 의 시간이 걸리기 때문에 삭제와 삽입이 잦은 상황에서 매우 효율적인 자료구조입니다. 이제, 이 자료구조를 직접 구현해 보겠습니다.

이중 연결 리스트의 노드는 `data` 와 함께, 자신의 이전 노드와 다음 노드의 위치를 가리키는 `prev`, `next` 를 가지고 있어야 합니다.

하나의 노드를 표현하는 구조체는 다음과 같이 구현할 수 있습니다.

### python3 코드

```python
class Node:
    def __init__(self, data):
        self.data = data # Linked list의 노드에 담을 데이터
        self.prev = None       # 초기에는 이전 노드와 다음 노드가 존재하지 않는다.
        self.next = None
```

이전 노드와 다음 노드가 없는 노드를 "단일 노드 (singleton)"라고 합니다.

하나의 정수를 가지는 단일 노드는 다음과 같이 생성할 수 있습니다.

### python3 코드

```python
class Node:
    def __init__(self, data): # 생성자 함수
        self.data: data
        self.prev = None
        self.next = None

node = Node(42)
```

## 단일 노드 삽입하기

어떤 연결 리스트에 속한 노드 `u` 뒤에 **단일 노드** `singleton` 을 삽입하는 작업은 다음과 같이 구현할 수 있습니다. 여기서, 단일 노드 `singleton` 은 노드 `u` 의 연결 리스트에 속하지 않아야 합니다. (이런 경우는 `singleton` 과 `u` 가 같을 때 뿐입니다.)

또한 구현 시, `None` 인 인스턴스의 속성에 접근하는 경우가 없도록 유의해야 합니다.

### python3 코드

```python
# 노드 u 뒤에 단일 노드 singleton를 삽입
def insert_next(u, singleton):
    # singleton의 prev와 next를 설정
    singleton.prev = u
    singleton.next = u.next

    # singleton의 이전 노드의 next와
    # 다음 노드의 prev를 설정       
    if singleton.prev is not None:
        singleton.prev.next = singleton
    if singleton.next is not None:
        singleton.next.prev = singleton
```

영상을 통해 자세한 과정을 살펴보세요.

![](https://contents.codetree.ai/problems/3996/images/introductions-d407950a-3472-427c-831c-c13944bb383f.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-7c9c881e-ab3f-415b-b6a5-6ef0e5976bec.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-491af99d-83b2-4414-8a40-6ca5225e8014.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ea1c3178-a54c-4686-bcfb-dbfed3caf05f.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-0abc95c4-148d-4d04-ab3c-f73daf6bddae.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ae1637c0-633b-4334-992d-ebb53ab1442d.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-a00f5b25-43fc-40fa-b0e8-6aa120eb810e.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-52a6402c-5a5f-4833-aaea-4f872b328d58.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-951da5e6-3763-4641-bf35-2a575cadddb4.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-527b0a40-94ca-4c0d-a086-842660d3bd27.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-dde41f67-03c2-4924-ae6f-b83b70f03688.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-4a7bd5f2-4222-48fe-9f5f-7bec3c249d1c.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-14a49268-baf6-4191-b720-0f6bc28ede85.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-64ca8044-b685-4e96-88ff-8cb7e4dfe03d.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ac84684d-1493-4606-94d8-2d03a3e42bd9.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ccd65ee8-ce02-48fe-8cbb-0be76d13b2eb.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ae437004-ecf1-4293-af30-e6cd9170b103.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-4e01fa9c-9bb1-4597-89c9-169dc19fdf06.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-7df5bb57-08ea-46f0-94aa-ad8eee3eec36.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-73702681-0c29-43bc-aa41-93ae3a4d832f.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-246e6833-54af-4516-8c65-fc1dd5536202.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-1f30ec05-34fa-4cf9-93ce-a4799ac88516.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-df00f882-92c4-47ec-9344-780ad89be4c9.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-3a2eb506-07c6-42dc-be65-784cf7cb13bd.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-241d93fe-7732-4ced-b505-705bd465c5e0.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-9422f679-78d9-4176-b44b-fa28ddc673b0.png)

1 / 26

비슷하게, 노드 `u` 앞에 **단일 노드** `singleton` 을 삽입하는 작업은 이렇게 구현할 수 있습니다. 여기서도, 단일 노드 `singleton` 은 노드 `u` 와 같은 연결 리스트에 속해 있으면 안됩니다.

구현의 마지막 네 줄이 `insert_next` 와 완벽히 같다는 사실에 주목하세요.

### python3 코드

```python
def insert_prev(u, singleton):
    singleton.prev = u.prev
    singleton.next = u
    
    # singleton의 이전 노드의 next와
    # 다음 노드의 prev를 설정
    if singleton.prev is not None:
        singleton.prev.next = singleton
    if singleton.next is not None:
        singleton.next.prev = singleton
```

영상을 통해 자세한 과정을 살펴보세요.

![](https://contents.codetree.ai/problems/3996/images/introductions-f831a21f-c64a-4c7e-a0a9-5238fe0c8cf8.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-9c238ed5-9561-4aed-b148-fe5fd278f157.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-33ea24dd-0ea1-4601-84a2-f89e1e7ebaa2.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-2c15c1e4-3a39-4554-8834-b47c9cb72b8b.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-c4074e80-86dc-445f-a398-211c96925f8d.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-d19b3e7d-2c18-418b-a8ea-2bbe2c46f02c.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-775ea164-68a2-4603-8b8e-6002320c7828.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-80113890-bff3-4901-b10c-6c3fba057ad8.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-bccedd83-20bb-4739-af56-53348db819c2.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-7fb9d866-c383-4c4a-b038-4c4b46145c40.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-d7de89a6-2cdc-4030-9af0-6fc861a06ef8.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-d713b5a8-4c30-4167-976e-207f906f0d4a.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-543dbd4c-d5b4-429a-9456-fc29fb337a27.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-847e1d61-773c-41b0-ad03-2f50fc2bf4e6.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-a8b4864c-5491-43bd-9ed3-3b7fa32ec5ec.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-db5c6649-20d3-46c0-bc54-fa6fd2a90d41.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-a3157784-6eb9-46dc-9ee2-1376bbd60880.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-32caeffb-88c9-4bc4-a599-fc2d55891d34.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-8808e70a-d52e-4bb4-8c0e-f3535a11f6c8.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-7728013d-bbfb-4872-9d9f-731d6d0e078c.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-e5e34f80-a303-4bc2-b0b9-3b98549cfa29.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-7a71d81b-0e07-40ab-9af7-ac03f7deb85a.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-1b206388-ef85-4774-92b9-93119dc76c1e.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-16848c00-493d-4dd6-9b75-b0ea04b08478.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-cff76406-0d51-4876-9c04-19caa81bbb37.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-6ca23640-f7d4-482e-821b-1ad06b930957.png)

1 / 26

## 노드 삭제하기

어떤 연결 리스트에 속한 노드 `u` 를 그 연결 리스트에서 삭제하면, 노드 `u` 는 단일 노드가 됩니다.

이 과정은 아래와 같이 구현할 수 있습니다.

### python3 코드

```python
def pop(u):
    # u의 이전 노드와 다음 노드를 서로 이어줌
    if u.prev is not None:
        u.prev.next = u.next
    if u.next is not None:
        u.next.prev = u.prev

    # 이제, u는 단일 노드가 됨
    u.prev = u.next = None
```

영상을 통해 자세한 과정을 살펴보세요.

![](https://contents.codetree.ai/problems/3996/images/introductions-61c01d18-b9c6-46b4-be86-133c47970faa.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-acd9cd56-bb28-45cf-be68-4410d1fffb88.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-50815c7b-dd9b-43b9-ba15-d4cbcd6b35ca.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-5e244718-4927-4699-92fd-1a8250a7bbc0.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-e05aad6f-8176-4eb9-92cc-406099e3795c.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-f6424237-50c9-4042-af22-869353add051.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-ba26771d-f6f6-4f42-a5b5-e5e0a4825d6e.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-e3b07694-015a-4e38-abf3-6dd68dca8739.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-d2b5e05a-e5ba-481b-bbd2-162bde81e404.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-b3a174a9-cc47-484a-8687-de344c8ef48c.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-3c8e8461-1a14-4a8e-98b2-b4e2832ad9db.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-23b6b25c-2c51-49a1-9e75-2f9d6db0ff1a.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-13196434-9328-4d88-839a-58fe4eb0a47d.png) ![](https://contents.codetree.ai/problems/3996/images/introductions-3e0ea3e6-95e5-4111-bcca-d3bc288086aa.png)

1 / 14

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.