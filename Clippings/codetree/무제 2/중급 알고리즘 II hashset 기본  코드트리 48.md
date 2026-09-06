---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-determine-subsequence/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Two Pointer

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 부분수열 여부 판단하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
두 수열 A와 B가 주어졌을 때 B가 A의 부분수열인지 판단하는 프로그램을 작성해보세요. 
B가 A의 부분수열이라 함은 B의 원소가 차례대로 A의 원소에 존재할 때를 의미합니다.

예를 들어 A = [5, 1, 5, 3, 1, 4] 일 때, B = [5, 1, 4] 라면 
5 1 4가 차례대로 수열 A에 존재하므로 B는 A의 부분수열입니다. 
하지만 만약 A = [5, 1, 5, 3, 1, 4], B = [3, 5, 1] 이라면 
3 5 1이 수열 A에 차례대로 존재하지 않으므로 B는 A의 부분수열이 아닙니다.
```

무작정 코드를 작성한다면, 수열 A에서 B의 원소들을 순서대로 뽑을 수 있는지를 재귀함수를 이용한 완전탐색 방법으로 판단해 볼 수 있을 것입니다. 위의 예시라면 B의 첫 번째 원소인 5를 수열 A의 원소에서 찾은 뒤, 그 뒤에서 다시 B의 두 번째 원소인 숫자 1을 찾고,... 이를 B의 마지막 원소까지 반복하는 것이 가능하면 부분수열임을 판단할 수 있는 것입니다.

이 과정은 수열 A가 1부터 N/2까지의 수가 순서대로 2개씩 놓여있는 `[1, 1, 2, 2, ...., N/2, N/2]` 구조이고, 수열 B가 `[1, 2, 3, 4, ...., N / 2, N]` 이런식으로 되어있는 경우라면 결국 부분수열은 아니겠지만 모든 가능한 경우를 다 탐색하게 될 것이므로 이를 판단하는데 $O(2^N)$ 의 시간이 소요될 것입니다.

이 방법에 대한 코드는 다음과 같습니다. 이 코드를 꼭 이해하고 넘어갈 필요는 없습니다.

```python
A = [0, 5, 1, 5, 3, 1, 4]
B = [0, 5, 1, 4]
n, m = 6, 3

def is_subsequence(a_idx, b_idx):
    # 수열 B의 마지막 원소까지 매칭이 끝났다면
    # 부분수열임을 확신할 수 있습니다.
    if b_idx == m + 1:
        return True
    
    # 수열 A의 원소들 중
    # 수열 B의 b_idx번째 원소와 일치하는 경우를 찾으면
    # 그 다음 원소들도 일치하는지를 확인합니다.
    for i in range(a_idx, n + 1):
        if A[i] == B[b_idx]:
            # 매칭 가능한 쌍이 있다면
            # 그 다음 원소부터 일치하는지를 확인합니다.
            is_possible = is_subsequence(i + 1, b_idx + 1)

            # 가능한 경우가 있다면 부분수열이라는 뜻입니다.
            if is_possible:
                return True

    # 전부 확인했음에도 가능한 경우가 없었다면
    # 부분수열이 아니라는 뜻입니다.
    return False

# 부분수열이라면 Yes를 출력합니다.
if is_subsequence(1, 1):
    print("Yes")
else:
    print("No")
```

이 문제를 좀 더 빠르게 해결해볼 수는 없을까요?

관찰을 통해 **수열 B의 원소들은 가능하면 수열 A의 가장 앞에 있는 원소와 매칭하는 것이 항상 이득** 이라는 점을 알 수 있습니다.

예를 들어 A = `[5, 1, 5, 3, 1, 4]` 일 때, B = `[5, 1, 4]` 인 경우라면 수열 B의 원소들을 수열 A의 앞에서부터 확인하며 일치하는 즉시 그 다음 원소를 비교하는 식으로 진행해도 부분수열임을 판단하는 데 충분하다는 뜻입니다.

![](https://contents.codetree.ai/problems/2204/images/introductions-45154d3c-6cc6-4176-b21c-fb4a6978ed1a.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-385f74b0-af27-4608-8623-bacea7b309e8.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-53cf752f-b88c-4bae-8ea7-c0ffbac30bb0.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-d428c505-c046-4664-88aa-8003a5483344.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-34a05259-aaa6-4672-8b81-c5c4a7c0e24f.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-10443c8d-7dec-467f-8bfb-8a210300d02d.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-65ae5b05-60ff-43ee-84e6-fab9c941487f.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-99d5d0f0-6c3e-4d44-9c3c-a8095e050f4e.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-fd36dba2-d2a7-47e3-80f4-ee2c483748b4.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-ab224f31-cac8-4f6a-8644-7e73df2ff477.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-c07ddbb3-dfe7-4a6c-a77c-8cbe45f2b97a.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-739428ec-f558-4f80-a8cb-2238149b93fa.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-aef23497-72f0-4ed6-8e32-4d351b7670be.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-781698c4-3bab-4d4d-b457-21e8b7d0c0fd.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-a5424f41-4eed-4b4b-808f-baad281c1938.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-dae2ea13-587b-4f20-b083-034cbeb1831c.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-6f2c2d14-aed0-43d4-ac9c-18aa99d9b194.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-61c0afa1-5790-4035-91e9-fd7e13ccdded.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-5face40d-0c8f-4156-bdc8-c8246806a1df.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-63e17b2d-9f41-453a-9c88-d4d1968b59a5.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-ec35c51b-efb8-4682-8097-9d77d50fc77e.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-212bc70f-a9ac-46b7-9023-31fe8f8ff424.png) ![](https://contents.codetree.ai/problems/2204/images/introductions-172e32a1-c1db-4452-9ce5-2240a93c9d07.png)

1 / 23

이 과정 역시 Two Pointer입니다. 다른 유형과는 다르게 i, j가 서로 다른 수열을 가리키고 있지만 같은 방향으로 계속 전진하는 구조이기 때문입니다. 따라서 부분 수열 판단 여부는 Two Pointer로 가능하며, 이 방법의 시간복잡도는 두 수열의 원소의 수를 각각 N, M이라 했을 때 두 길이의 합인 $O(N + M)$ 이 됩니다.

코드는 다음과 같습니다.

```python
A = [0, 5, 1, 5, 3, 1, 4]
B = [0, 5, 1, 4]
n, m = 6, 3

def is_subsequence():
    i = 1
    # B의 원소를 기준으로
    # 순서대로 매칭이 가능한지를 확인합니다.
    for j in range(1, m + 1):
        # A의 원소가 B의 j번째 원소와
        # 일치해지는 위치를 구해줍니다.
        while i <= n and A[i] != B[j]:
            i += 1
        
        # 만약 수열 A에서 일치하는 원소를 찾지 못햇다면
        # 부분수열이 아닙니다. 
        if i == n + 1:
            return False
        # 일치한다면
        # A 원소의 위치도 한칸 앞으로 이동시켜 줍니다.
        else:
            i += 1

    # 전부 매칭하는게 가능했다면
    # 부분수열입니다.
    return True

# 부분수열이라면 Yes를 출력합니다.
if is_subsequence():
    print("Yes")
else:
    print("No")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.