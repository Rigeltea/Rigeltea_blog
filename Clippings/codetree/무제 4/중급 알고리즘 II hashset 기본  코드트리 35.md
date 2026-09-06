---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-duplicate-sequence/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. Trie

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Trie

6개의 문자열 "app", "apple", "apply", "apart", "ban", "banana"이 주어졌다고 생각해봅시다. 여기서 "ap"로 시작하는 서로 다른 문자열의 수를 구하기 위해서는 각 문자열과 일일이 비교를 해봐야 할 것입니다.

```python
# 주어진 문자열
words = ["app", "apple", "apply", "apart", "ban", "banana"]
# 찾고자 하는 문자열 (prefix)
target = "ap"

# 찾고자 하는 문자열의 길이
m = len(target)

cnt = 0
for word in words:
    # prefix가 target과 일치하는 경우라면
    # 수를 세어줍니다.
    if word[:m] == target:
        cnt += 1

print(cnt)
```

만약 주어진 문자열의 개수를 n, 비교할 문자열의 길이를 m이라 한다면 각 문자열에 대해 비교 문자열의 길이만큼 순회하며 정확히 일치하는지를 판단해야 하므로 위 방법의 시간복잡도는 $O(NM)$ 이 될 것입니다.

이때 Trie라는 자료구조를 사용하면 특정 문자열로 시작하는, 즉 특정 문자열을 접두사(prefix)로 하는 서로 다른 문자열의 수를 특정 문자열의 길이에 해당하는 $O(M)$ 만에 구할 수 있습니다.

Trie는 주어진 문자열들을 트리 형태로 나타낸 자료구조입니다. 예로 "app", "apple", "apply", "apart", "ban", "banana" 문자열들로 나타낸 Trie의 모습은 아래와 같습니다.

![](https://contents.codetree.ai/problems/1943/images/introductions-6302ce41-8675-4890-bf10-b53505b07799.png)

Trie는 Root에서 시작합니다. 각 문자열에 대해 루트에서 시작하여 문자열 내 문자 순서대로 각 문자를 간선으로 하여 트리를 만들어 나갑니다. 만약 "app"을 먼저 Trie에 추가하게 되면 다음 그림이 만들어집니다.

![](https://contents.codetree.ai/problems/1943/images/introductions-f005d8b4-a330-4e30-9f08-49151141abb2.png)

맨 끝 노드에 색칠을 해주는 이유는 해당 노드가 특정 문자열의 맨 끝임을 표시하기 위함입니다. 이는 다양한 문제를 해결하는 데 있어 큰 도움이 됩니다.

그 다음 "apple"이라는 문자열을 Trie에 추가하게 되면 다음과 같이 a, p, p는 같은 노드를 사용하게 되고, l, e에 해당하는 새로운 노드가 생겨나게 됩니다.

![](https://contents.codetree.ai/problems/1943/images/introductions-008411cf-d1fe-4f91-822a-7d1c063126ef.png)

이런 방식으로 "app", "apple", "apply", "apart", "ban", "banana" 문자열들을 순서대로 Trie에 추가하여 구성하는 과정은 아래와 같습니다.

![](https://contents.codetree.ai/problems/1943/images/introductions-60003e6e-45d8-4027-a0e8-4e586c2f988c.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-2c60c26b-216a-4f3c-bafe-574298174112.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-69a7dd19-a940-4ca8-87b7-2a1b5847ede1.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-1a4bab59-b382-4c06-96b9-eb7a6be04ac1.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-48e19e0e-cb74-45e9-a86c-c3bd3b3f8cf0.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-6a85b07e-f640-47f9-b374-6fce14afce9c.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-dc095698-6cb9-467f-86b9-66f884e21c51.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-a81cbd07-f5d5-4d56-96b4-80b0dc2765b7.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-afaf41dc-3415-450c-a26a-1f305dbdc12e.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-e89c7bd7-b7cf-4e52-a840-563145ca104f.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-399b87c5-bf81-417c-a790-b96405437175.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-8d51298a-8f9c-4af3-8ce7-1780dad74db5.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-aa9a48f5-c1d7-48f1-81fc-bb003b5bb7c3.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-92d60792-e574-4219-8f19-048fe8377743.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-17364167-dc4e-4a37-bc5b-e71abb48d011.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-b3e2a551-8479-44d2-9f68-8ffcd64b0b5e.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-672a1329-5a22-41fa-9fab-6d10516e6f84.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-bc80c249-da3b-444f-a1fe-1faee7cc2c59.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-cd1993ca-ec3f-46f5-b7c7-f0cf71a02776.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-d2da5d95-1d93-4ccf-8828-e4e05c0ba689.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-c041689e-9b90-430f-9a68-8e69f051a6fd.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-9f5875d4-34e3-4804-b966-520972acaccf.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-97d881c9-c1f5-43cc-878f-1fcc07ad32be.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-704aa907-897d-4c1b-b998-14d9d6ceca84.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-7fa69e85-c41a-4afb-b042-43aa48a9a546.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-0cf843bb-c30d-4449-af3b-f58ebd31afb8.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-7255cc2c-2ffc-4a63-b7ac-eb99b4ecd656.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-c642329a-d55f-4637-b752-ca5e2287bd5e.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-efb8c853-9a31-4186-b3fc-144156fb7e95.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-0048b2fa-5b0b-43a8-91be-1bf43729ad3b.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-7a6079da-a137-4e2a-9103-328440c51aa7.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-693fb0bb-1a37-4178-a9f2-e31b3d32851f.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-2f24ede6-8908-473e-833a-ea81bd900a1c.png) ![](https://contents.codetree.ai/problems/1943/images/introductions-032cba57-ba1c-4580-9e32-df7615a6c3f9.png)

1 / 34

Trie를 만들기 위해서는 모든 문자열 내 문자를 한번씩만 순회하면 됩니다. 즉, 모든 문자열 길이의 합을 L이라 했을 때 시간복잡도는 $O(L)$ 이 됩니다.

이렇게 Trie를 만들어주는 코드는 아래와 같습니다. TrieNode라는 새로운 class를 만들어 각 노드마다 자식들을 26개 관리하고 (소문자 'a'부터 소문자 'z'까지 순서대로 0~25까지의 인덱스로 관리), 문자열의 끝임을 표시해주기 위해 is\_end라는 값을 설정해줍니다.

```python
# 변수 선언 및 입력:
words = ["app", "apple", "apply", "apart", "ban", "banana"]

# Trie에 사용되는 노드를 정의합니다.
class TrieNode():
    # 생성자입니다.
    def __init__(self):
        # 해당 노드를 기점으로 하나의 단어가 완성되는지를 판단합니다.
        # 단어 완성에 대한 초기값은 False입니다.
        self.is_end = False

        # 각 노드에는 'a'부터 'z'까지의 문자에 대응되는 26개의 노드 정보가 관리됩니다.
        # 각 문자에 대응되는 노드 정보는 처음에 None이 됩니다.
        self.children = [None for _ in range(26)]

# 루트 노드에 해당하는 TrieNode를 처음 만들어줍니다.
root = TrieNode()

# 단어 s를 Trie에 넣어줍니다.
def insert_word(s):
    # root에서 시작합니다.
    t = root
    for char in s:
        # 문자 순서대로 따라가면 됩니다.
        # 'a'부터 'z'까지 사용되므로
        # 각각을 0부터 25까지의 index로 매핑시켜줍니다.
        index = ord(char) - ord('a')
        # 해당하는 노드가 아직 없다면 새로운 노드를 만들어줍니다.
        if t.children[index] is None:
            t.children[index] = TrieNode()
        
        # index에 해당하는 노드로 옮겨갑니다.
        t = t.children[index]
    # 최종 위치에 단어의 끝임을 표시해줍니다.
    t.is_end = True
   
# Trie에 단어들을 넣어줍니다.
for word in words:
    insert_word(word)
```

이렇게 Trie를 만들게 되면 어떻게 "ap"로 시작하는 서로 다른 문자열의 수를 빠르게 구할 수 있게 될까요?

이제 Trie에서 "ap"라는 키워드로 검색을 진행해보겠습니다. 비교할 문자열의 길이를 m(여기서는 "ap"의 길이인 2)이라 했을 때 Trie에서 "ap"를 따라가는데 걸리는 시간은 $O(M)$ 입니다.

![](https://contents.codetree.ai/problems/1943/images/introductions-7e0aaacc-09ab-47c9-81b2-ec01dba951d2.png)

이제 $O(M)$ 에 위와 같이 ap의 위치를 찾았습니다. 그러면 "ap"로 시작하는 서로 다른 문자열의 수는 **이제 "ap"에 해당하는 노드의 자손들 중 빨간색으로 색칠된 노드의 개수가 됩니다.** 그 이유는 Trie는 prefix에 대한 tree이며 색칠된 노드는 문자열의 끝을 나타내기 때문입니다.

각 노드마다 자손들 중 빨간색으로 색칠된 노드의 수는 트리 노드의 수가 $O(L)$ 이기에 미리 Tree에서 DP를 적용하여 전처리로 값을 $O(L)$ 에 구해놓을 수 있습니다. 아직 [Tree DP](https://www.codetree.ai/missions/9/problems/calculating-an-integer-for-a-node/introduction) 유형에 대해 잘 모르신다면 해당 유형을 공부하신 후 이 내용을 다시 읽는 것을 추천드립니다.

따라서 Trie를 구성하면 이후 특정 문자열을 접두사로 하는 문제를 효율적으로 해결할 수 있게 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.