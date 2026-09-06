---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-number-of-distinct-segments/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. +1-1 technique

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 선분의 시작과 끝을 활용한 테크닉

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
다음과 같이 1차 수직선상에 총 6개의 구간이 주어졌을 때,
이 구간을 모두 합친 이후 남아있는 서로 다른 구간의 수를
구하는 프로그램을 작성해보세요.
```

![](https://contents.codetree.ai/problems/2275/images/introductions-8fcf0653-b87c-4c74-a391-e42fdecab746.png)

위의 그림에서의 답은 다음과 같이 2가 됩니다.

![](https://contents.codetree.ai/problems/2275/images/introductions-47fbdf55-2f76-4d79-a755-1dfa088254c7.png)

눈으로 봤을 때는 지극히 당연히 2개라는 것을 알 수 있지만, 이를 컴퓨터가 계산하기 쉽게 나타내기 위해서는 어떻게 해야 할까요?

이는 마찬가지로 +1-1 Technique으로 해결이 가능합니다. 다만 실제 +1, -1을 진행하는 것이 아닌, 각 선분들을 시작점과 끝점으로 구분하여 x좌표 순으로 정렬하여 해결할 수 있습니다. 순서대로 보다가 **노란색이 나왔을 경우 중, 남아 있는 선분이 없었다면 구간의 시작이라는 뜻이므로 이때의 가짓수를 세면 됩니다.** 보라색이 나왔을 경우에는, 해당 선분을 제외시켜주면 됩니다. 각 선분을 넣고 제외시켜주는 과정은 hashset을 이용하면 쉽게 구현이 가능합니다. 이 문제에서는 hashset을 꼭 쓰지 않아도 풀리기는 하지만, 의미상 어떤 선분이 골라졌는지를 보여드리기 위해 각 선분 정보를 hashset에 넣어서 관리하도록 하겠습니다.

![](https://contents.codetree.ai/problems/2275/images/introductions-77b26869-cc25-4ed5-b06e-b8509d2bed27.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-4caac929-4b56-4481-b668-888bac566db4.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-8847774e-331f-4667-a5fd-425705ad35c3.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-39aa9b42-a057-4f5e-b837-0f47c203c91e.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-06d093f1-30fc-4427-8618-4f353cca7507.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-030b8c39-0622-47dc-bbc4-d78b2d106406.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-290ed50e-f7c8-40cb-9ba1-7e863bcafd7c.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-7d910cf9-8272-4c47-9565-8fe51bcde360.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-bab3a1ad-3c6b-44ff-9e1f-b3e2bf3eaa39.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-2fd69bb3-9259-4a4b-8b72-9d6441a3432a.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-3f6108e6-a955-408a-83b2-91903e5f6930.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-d0e5a680-2002-4298-ab79-27febffca463.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-ca42810a-2951-4170-a2bd-712012f0b847.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-4079a442-a2c2-4903-b6e0-9b170e7943a8.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-ca305d89-cd20-4b09-b51f-55c9c99066bb.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-85d5b078-f80e-4db0-afbf-8d336c84f5f9.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-2f55b9e0-ea16-43a6-a895-8959e710afa6.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-b02b6051-dfec-4a28-8f7d-42cdfac277bc.png) ![](https://contents.codetree.ai/problems/2275/images/introductions-7a6da787-39bd-4062-bf7f-5ad2f470ddec.png)

1 / 19

2N개의 정점을 정렬하는데 $O(NlogN)$ 의 시간이 걸리고, 이후 2N개의 점을 순차적으로 보며 진행하면 되므로 $O(N)$ 이 걸리기 때문에 총 시간복잡도는 $O(NlogN)$ 이 됩니다.

코드는 다음과 같습니다. 각 선분이 아직 남아 있는지를 판단하기 위해, 각 선분의 정보를 정렬할 때 **각 선분의 번호도 포함하여** 정렬해줘야 함에 유의합니다.

```python
segments = [
    (1, 5), (4, 7), (3, 6), (9, 13), (8, 15), (12, 16)
]
n = 6

# 각 선분을 두 지점으로 나눠 담은 뒤,
# 정렬해줍니다.
# 이때 (x좌표, +1-1값, 선분 번호)
# 형태로 넣어줍니다.
# +1은 시작점
# -1은 끝점을 뜻합니다.
points = []
for i, (x1, x2) in enumerate(segments):
    points.append((x1, +1, i)) # 시작점
    points.append((x2, -1, i)) # 끝점

# 정렬을 진행합니다.
points.sort()

# 각 점을 순서대로 순회합니다.
# 등장하고 아직 사라지지 않은
# 선분을 hashset으로 관리합니다.
segs = set()

ans = 0 # 서로 다른 구간의 수를 저장합니다.
for x, v, index in points:
    # 시작점인 경우입니다.
    if v == +1:
        # 남아있는 선분이 없다면
        # 답을 갱신합니다.
        if not segs:
            ans += 1
        
        # 해당 선분 번호를 hashset에 넣어줍니다.
        segs.add(index)

    # 끝점인 경우입니다.
    else:
        # 해당 선분을 제거합니다.
        segs.remove(index)

# 서로 다른 구간의 수 = 2
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.