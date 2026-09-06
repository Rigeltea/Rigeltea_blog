---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-max-interval-without-overlapping-numbers/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Two Pointer

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Counting Array와 Two Pointer

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[2, 1, 2, 2, 1, 3, 1] 와 같이 숫자들이 주어졌을 때,
특정 구간을 잘 골라 구간 내 같은 숫자가 3개 이상 있지 않은 경우 중
가장 큰 구간의 크기를 구하는 프로그램을 작성해보세요.
```

이 문제에서 각 구간의 시작점을 i로 잡았다고 했을 때, 같은 숫자가 3개 이상이 되지 않도록 최대로 뻗어나갔을 때의 구간의 끝점을 j로 하여 그림을 그려보면 다음과 같습니다.

![Image](https://contents.codetree.ai/problem_factory/images/02363112-f5ea-42aa-844a-f4d5c9a576ce.webp) ![Image](https://contents.codetree.ai/problem_factory/images/f7ca87b3-aa88-436c-b0f9-e876b572ea0f.webp) ![Image](https://contents.codetree.ai/problem_factory/images/d6be4618-07f8-47a3-960f-ee0e87995f95.webp) ![Image](https://contents.codetree.ai/problem_factory/images/d91ea990-8afe-457d-a566-0cb463b6acff.webp)

1 / 8

즉, 시작점 i에 대해 어디까지 진행해도 되는지를 빠르게 판단할 수 있다면 Two Pointer 방법으로 풀린다는 것을 알 수 있습니다.

이러한 상황에 유용하게 사용될 수 있는 기법이 바로 Counting Array입니다. 각 숫자마다 몇 번씩 나왔는지를 counting 해주는 배열을 추가적으로 만들어 관리하면, 현재 `[i, j]` 구간 내 각 숫자가 몇개 씩 들어있는지를 계속 tracking할 수 있기 때문에 j를 더 증가시키기 전에 현재 $A_{j + 1}$ 이 더 추가되면 같은 숫자가 3개가 되지는 않는지를 $O(1)$ 로 즉각적으로 확인해볼 수 있게 됩니다.

다음 그림은 i = 2, j = 6인 시점에서 Counting Array의 1번 index를 확인하여 숫자 1이 이미 2번 나왔으므로 j가 더 이상 진행할 수 없음을 깨닫고 움직이는 것을 멈추는 예시입니다.

![](https://contents.codetree.ai/problems/2214/images/introductions-0fa7ffd6-c96d-4e5e-baff-818db6c1d9d6.png)

Counting Array를 이용해 각 숫자가 현재 구간 내에 몇 번씩 등장하는지를 기록하고 확인하는 데에는 시간이 $O(1)$ 이므로, Two Pointer 테크닉을 이용하면 $O(N)$ 에 문제에서 원하는 최대 구간의 크기를 구할 수 있게 됩니다.

**주의:** 아래 슬라이드는 최대 중복을 1개까지만 허용한 예시이고, 코드는 처음 예시대로 최대 중복을 2개까지만 허용한 코드입니다.

![Image](https://contents.codetree.ai/problem_factory/images/365c4bea-7964-44ab-af06-05d5564038fe.webp) ![Image](https://contents.codetree.ai/problem_factory/images/9af1ed98-8db2-4d56-af51-914c7a9428ba.webp) ![Image](https://contents.codetree.ai/problem_factory/images/ec8d784b-900f-4d15-adb5-c7770cd520e4.webp) ![Image](https://contents.codetree.ai/problem_factory/images/7da642c3-daf9-4f19-81c0-8ef73e89d17d.webp) ![Image](https://contents.codetree.ai/problem_factory/images/ba9eac58-d485-487d-9b85-d49fe67ec569.webp) ![Image](https://contents.codetree.ai/problem_factory/images/0aaa2f1a-2e80-4e3a-8930-a77605b895cd.webp) ![Image](https://contents.codetree.ai/problem_factory/images/5514415e-69a5-4de8-b20e-d9eff62e571e.webp) ![Image](https://contents.codetree.ai/problem_factory/images/a35d1c6a-fc10-4939-a003-0a4aafcdd242.webp) ![Image](https://contents.codetree.ai/problem_factory/images/4d3be6c4-0b3f-43ca-9a2c-6000aba6199d.webp) ![Image](https://contents.codetree.ai/problem_factory/images/80e8a908-4084-4df9-9788-48c0309d216e.webp)

1 / 19

코드는 다음과 같습니다.

```python
arr = [0, 2, 1, 2, 2, 1, 3, 1]
count_array = [0] * 4
n = 7

# 가능한 구간 중 최대 크기를 구합니다.
ans = 0

# 구간을 잡아봅니다.
j = 0
for i in range(1, n + 1):
    # 같은 숫자가 3개가 되기 전까지 계속 진행합니다.
    while j + 1 <= n and count_array[arr[j + 1]] != 2:
        count_array[arr[j + 1]] += 1
        j += 1
    
    # 현재 구간 [i, j]는 
    # i를 시작점으로 하는
    # 가장 긴 구간이므로
    # 구간 크기 중 최댓값을 갱신합니다.
    ans = max(ans, j - i + 1)

    # 다음 구간으로 넘어가기 전에
    # arr[i]에 해당하는 값은 count_array에서 지워줍니다.
    count_array[arr[i]] -= 1

# 조건을 만족하는 가장 큰 구간의 크기는
# [1, 2, 2, 1, 3]로 5가 됩니다.
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.