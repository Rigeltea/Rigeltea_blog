---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-switch-position-in-array/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Doubly-LinkedList

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 연결 리스트의 연속한 노드들을 제거한 후 삽입하기

이제, 노드 `s` 에서 노드 `e` 까지의 연속한 노드들을 연결 리스트에서 제거한 후, 노드 `v` 의 앞에 추가하는 작업을 구현해봅시다.

먼저, 다음과 같은 중요한 가정들이 반드시 지켜져야 합니다.

- 두 노드 `s` 와 `e` 는 같은 연결 리스트에 속해야 합니다.
- 그 연결 리스트에서 노드 `s` 가 노드 `e` 보다 앞에 위치해야 합니다.
- 노드 `v` 는 `s` 부터 `e` 까지의 연속한 노드들에 속하면 안됩니다.

### Step 1. 연결 리스트에서 s부터 e까지의 노드들을 제거하기

`s` 의 이전 노드와 노드 `e` 의 다음 노드를 서로 이어주면 충분합니다.

### Python3 코드

```python
def pop_range_and_insert_prev(s, e, v):
    # s의 이전 노드와 e의 다음 노드를 이어줌
    if s.prev is not None:
        s.prev.next = e.next
    if e.next is not None:
        e.next.prev = s.prev
    
    # 이제, s의 이전 노드와 e의 다음 노드를 nullptr로 설정
    s.prev = e.next = None

    # 이어서...
```

동영상을 통해 더 자세하게 이해해보세요.

![](https://contents.codetree.ai/problems/3998/images/introductions-a45e6d43-d861-4026-99da-5e33b15a3085.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-8fdaeca8-ad7a-4315-aa9f-f890bba01c68.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-ef046bf9-8289-4f22-b1d0-4ab648ec961e.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-99cb486e-e44e-4427-aa3d-05d70037e4ad.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-13290c7b-79d0-43eb-aae3-666a12116f1b.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-997eb742-ada5-444d-abf6-9cb784e36eed.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-dda73d69-ae59-495f-8bf2-0d673436d317.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-97d94dd4-ce2d-46de-8d31-9e69d1c276e4.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-e75c7741-5e78-409f-badb-28116a45c4dc.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-1b0fbc59-81de-46fb-8472-fda9b2ae1734.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-b8c8a871-f904-4591-bb16-b4eb5760bf70.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-231c904a-5d2c-4ff0-9678-643e191db718.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-83955a52-15b3-4773-b832-ee33b79f8d7c.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-1222ab2a-1626-4713-83d2-a75ab73eff34.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-aad5ac77-1e2c-4d98-be56-94b563955e40.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-5484d83a-81a4-421a-b5e6-29323a6c99c4.png)

1 / 16

### Step 2. s부터 e까지의 노드들을 v 앞에 삽입하기

이제, `s` 부터 `e` 까지의 노드들은 하나의 연결 리스트를 구성하고 있습니다. 즉, 이 연결 리스트의 head는 노드 `s` 이고, tail은 노드 `e` 입니다. (이중 연결 리스트의 head와 tail의 개념은 [이 글](https://www.codetree.ai/missions/6/problems/singly-and-doubly/introduction) 을 참고하세요.)

![](https://contents.codetree.ai/problems/3998/images/introductions-e95e22c7-0abd-4b32-9c3e-97ff04a7cf27.png)

다음 그림과 같이 head는 이중 연결 리스트의 제일 앞 노드이며, tail은 이중 연결 리스트의 제일 뒤에 있는 노드입니다.

`v` 의 이전 노드와 `v` 사이에 `s` 부터 `e` 까지의 노드들을 삽입해야 합니다.

이 과정은

- `v` 의 이전 노드와 `s` 를 서로 이어주고
- `e` 와 `v` 를 서로 이어주면

충분합니다.

### Python3 코드

```python
def pop_range_and_insert_prev(s, e, v):
    # ...
    # Step 1의 구현 끝
    
    # v의 이전 노드와 s를 이어줌
    if v.prev is not None:
        v.prev.next = s
    s.prev = v.prev
    
    # e와 v를 이어줌
    e.next = v
    v.prev = e
```

동영상을 통해 더 자세하게 이해해보세요.

![](https://contents.codetree.ai/problems/3998/images/introductions-81b7e95b-43ab-4e01-a430-d3d655def833.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-db2a0536-8a86-4b12-9d50-a85652768380.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-e3ae262c-3df7-481a-91d6-a193c4400032.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-92c91249-0efd-4bd8-935f-086febd58af7.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-84d5d270-fdf7-46ed-96b3-139ac131de9a.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-a854ba68-ef31-4efe-84d3-241cc90c6fe5.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-7cc249f7-1f16-4a07-89fb-e62b9543af1a.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-9f250611-a32d-40f3-a850-c34ad01945b3.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-b5356a98-ccd9-4099-bd0a-ddd1ee18b7e3.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-6018ae2f-5d5b-4cd8-b58a-d43e07231108.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-3236b26c-ca96-4a84-85c0-0a014255b632.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-1e4856ce-7a36-48fd-9ddd-6fe7e7be81cb.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-f0be6337-e6dd-4d88-84a1-2b2b47d289a3.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-0e2bd525-242b-4c0d-9378-e926de36180d.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-baa7c103-9f93-4566-b587-0f9ca0310d41.png)

1 / 15

### 완성된 코드

```python
def pop_range_and_insert_prev(s, e, v):
    # Step 1
    # s의 이전 노드와 e의 다음 노드를 이어줌
    if s.prev is not None:
        s.prev.next = e.next
    if e.next is not None:
        e.next.prev = s.prev
    
    # 이제, s의 이전 노드와 e의 다음 노드를 nullptr로 설정
    s.prev = e.next = None

    # Step 2
    # v의 이전 노드와 s를 이어줌
    if v.prev is not None:
        v.prev.next = s
    s.prev = v.prev
    
    # e와 v를 이어줌
    e.next = v
    v.prev = e
```

지금처럼 이중 연결 리스트와 관련된 기능을 구현할 때, 두 노드를 서로 이어주는 작업은 앞으로도 자주 등장할 것입니다. 이 작업을 배열에서 수행하면 시간 복잡도는 $O(N)$ 이 되지만, 이중 연결 리스트를 사용하면 $O(1)$ 이 됨을 관찰하세요.

위의 코드에서 (`Null` 일 수도 있는) 두 노드를 이어주는 함수 `connect` 를 사용하면 더욱 간결하게 작성할 수 있습니다.

### Python3 코드

```python
def connect(s, e):
    # s와 e를 이어줌
    if s is not None:
        s.next = e
    if e is not None:
        e.prev = s
```

connect 함수를 동영상을 통해 더 자세하게 이해해보세요.

![](https://contents.codetree.ai/problems/3998/images/introductions-f3aad454-2571-40f7-94e8-aecacdeb1112.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-5fb19033-4d6c-4e15-ae30-7b41ea7db27d.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-3862265e-91ff-4f57-aede-565d3749dd55.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-eac199a8-9cd3-4f13-b679-22a2f42ad5d7.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-a4c190d1-7d9e-4a4f-a325-c399c162ae35.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-5a2c7f8b-0023-41be-8fc8-e56ced65738f.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-5ff74dc5-ac8c-425a-a033-ef56ee64654f.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-c81245c3-c752-468a-9821-21ac69aeed9b.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-32e83d87-e6c2-4ff4-b4c3-9fbf1b17416d.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-c0415bab-6056-4830-b547-2b054c3075cc.png)

1 / 10

  
최종적으로 connect 함수를 사용해 구현한 코드는 다음과 같습니다.

```python
def connect(s, e):
    # s와 e를 이어줌
    if s is not None:
        s.next = e
    if e is not None:
        e.prev = s

def pop_range_and_insert_prev(s, e, v):
    # Step 1
    # s의 이전 노드와 e의 다음 노드를 이어줌
    connect(s.prev, e.next)

    # 이제, s의 이전 노드와 e의 다음 노드를 nullptr로 설정
    s.prev = e.next = None

    # Step 2
    # v의 이전 노드와 s를 이어줌
    connect(v.prev, s)
    
    # e와 v를 이어줌
    connect(e, v)
```

간략해진 코드를 동영상을 통해 더욱 더 자세하게 이해해보세요.

![](https://contents.codetree.ai/problems/3998/images/introductions-7721f6d3-3ccd-4620-805e-289e39a08157.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-8e14c898-2402-4db2-9890-ae86179452ba.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-b70c5cc5-e112-4064-b0b4-f53846658aec.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-61d9752f-8d22-4d2e-9c4b-6b1392f33ff6.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-743cbd71-bb4f-4f0b-9bb1-ea2fc4da9ae3.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-68f37e83-e550-49d2-a2a0-3d2266898132.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-f37205b8-b89e-4214-be0b-14b295ca24b3.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-c5041d22-d842-41c9-a9c6-5ce8851ca6cb.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-98ff2fbb-4ad0-4e29-8e03-40943c760343.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-df0cb73e-5e9f-4248-88e9-e66120fa2a40.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-e3219ac5-9601-42ee-be25-dc7006a93a29.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-4a576012-a723-403b-833d-d5b53e7b18b9.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-39886cde-148b-4f4f-9e42-9ac2b8eca6e0.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-0a865a5f-10ea-4c80-b7d7-7eb8bd3400cc.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-6e248f3d-c7ca-4be9-8b6e-bd4296e91f7c.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-56053f19-a274-4812-a69e-59ccb4bbf409.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-410d70de-68f1-41b8-93fd-1c6cfda6fbf4.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-cb714831-f518-4c55-9fb1-02cfc89e6932.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-c84da5a0-6d52-4fef-9ca4-3a5cbdb9e3de.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-e9de8b03-dddc-4338-91c1-2ad0de35d8fb.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-bbb08c4d-080a-4518-8c88-07ce4676f9bf.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-626a9c82-43c8-45a6-9784-09da1012856c.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-8bb78227-d587-4ea7-b783-4a8f9e5c80ac.png) ![](https://contents.codetree.ai/problems/3998/images/introductions-291b2e34-2e35-4a27-b7c4-e45c1e4455c1.png)

1 / 24

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.