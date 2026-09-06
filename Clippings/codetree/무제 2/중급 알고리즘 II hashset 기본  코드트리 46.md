---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-shortest-subtotal/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Two Pointer

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Two Pointer

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[6, 3, 2, 4, 9, 1] 와 같이 숫자들이 주어졌을 때,
특정 구간을 잘 골라 구간 내 숫자의 합이 10을 넘지 않으면서
가장 큰 구간의 크기를 구하는 프로그램을 작성해보세요.
```

무작정 코드를 작성한다면, 모든 구간 $O(N^2)$ 개를 잡아보면서 그 안에 있는 숫자를 전부 더해 합이 10을 넘지 않는 경우 중 구간 크기의 최댓값을 구하면 되므로 $O(N^3)$ 이 소요됩니다.

이 방법에 대한 코드는 다음과 같습니다.

```python
arr = [0, 6, 3, 2, 4, 9, 1]
k = 10
n = 6

# 가능한 구간 중 최대 크기를 구합니다.
ans = 0

# 모든 구간을 탐색합니다.
for i in range(1, n + 1):
    for j in range(i, n + 1):
        # 구간 내 합을 구합니다.
        sum_val = 0
        for l in range(i, j + 1):
            sum_val += arr[l]

        # 구간 내 합이 10 이하라면,
        # 구간 크기 중 최댓값을 갱신합니다.
        if sum_val <= k:
            ans = max(ans, j - i + 1)
    
# 조건을 만족하는 가장 큰 구간의 크기는
# [3, 2, 4]로 3이 됩니다.
print(ans)
```

이때 구간을 정한 뒤 구간 내 합을 구할 것이 아니라, 구간 내 **시작점 i** 를 정하고 시작점 i로부터 합이 10을 넘지 않는 가장 멀리 있는 **구간의 끝 j** 를 정하는 식으로 진행한다면, $O(N^2)$ 으로도 문제에서 원하는 최대 구간의 크기를 구할 수 있습니다.

![](https://contents.codetree.ai/problems/1310/images/introductions-1f63071c-7f28-496b-9698-27785988549e.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-053c3e2b-7b91-4885-a8c7-67b8a244340b.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-6a9f0063-598c-4758-bc30-60ad18fda4f9.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-51c40479-39da-40b3-9c39-99279ab2a970.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-e5df2e78-f17d-4170-a88a-16258e7ca044.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-e761cbdc-5560-46b0-aa34-223b1f445a8f.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-8d063837-58c5-41bd-86c6-2a0c6dda37d0.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-1fb43213-bbe7-4e5e-a4b1-2dc147300332.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-4beae5b7-cad9-4c83-bd14-9851bb10c846.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-f7e80953-b80e-478e-925e-85c09f53eb44.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-d06af707-de12-401a-85a1-913c3b2be04f.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-67debf9b-91f9-446e-8e5a-9603168e7b65.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-ea1f2eb7-7b19-4a72-be0e-8bb071192402.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-e7025530-9bc3-4a27-92ef-793613312d06.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-d621aaf7-26ca-4f6a-a4ed-0cdca0250415.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-a946aa67-e041-4697-af49-14ceb4b36c29.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-15c1b529-638a-4ba5-a7dc-3c9d544a8c3d.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-b991242e-9ffa-492f-85a0-1a193dfcf645.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-a6531f59-d6f9-4ddc-97eb-0341293feae0.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-fd34e68f-ac61-434d-aa93-08375ace6dee.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-164bedae-d5c3-4162-acb2-b8ce32e7d5ac.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-e069f0b0-df89-4e4f-91e7-41d7d8750afc.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-c6bedec2-358f-4f54-886a-544cb4364c53.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-d199179b-27c6-474e-aefd-a81b5038d2f5.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-6c706c9d-9f18-4c80-b7b8-63b23e0c5d83.png)

1 / 25

이 방법에 대한 코드는 다음과 같습니다.

```python
arr = [0, 6, 3, 2, 4, 9, 1]
k = 10
n = 6

# 가능한 구간 중 최대 크기를 구합니다.
ans = 0

# 모든 구간을 탐색합니다.
for i in range(1, n + 1):
    # 구간 내 합이 10을 넘지 않을때까지 계속 진행합니다.
    sum_val = 0
    for j in range(i, n + 1):
        sum_val += arr[j]
        
        # 구간 내 합이 10을 넘게되면 그만 진행합니다.
        if sum_val > k:
            break

        # 현재 구간 [i, j]는 
        # 유효한 구간이므로
        # 구간 크기 중 최댓값을 갱신합니다.
        ans = max(ans, j - i + 1)

# 조건을 만족하는 가장 큰 구간의 크기는
# [3, 2, 4]로 3이 됩니다.
print(ans)
```

그런데 구간의 시작점 i가 고정되었을 때, 최대로 뻗어 나갈 수 있는 구간의 끝 j를 전부 살펴보았을 때 어떤 규칙이 보이지 않으신가요?

![](https://contents.codetree.ai/problems/1310/images/introductions-ae9ae477-6177-4e4d-9b5a-63290642a8b7.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-c7a66ee1-9ca9-4ec4-8d36-42583fcada22.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-f3736448-5bfb-45ec-98ca-292bce62ffbb.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-bf545630-41af-4b08-9f33-a8f68671f2e6.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-b141c524-f40a-4f26-963d-1856ba882147.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-364304d7-32d8-43b2-89e1-57ea896450cb.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-97c75efe-424f-479c-915e-cdc3c32e384d.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-1742dcc1-b778-479f-810c-4fd145c6d62f.png)

1 / 8

그렇습니다. **i가 1씩 늘어날 때마다, 최대로 뻗어나갈 수 있는 j의 위치는 항상 같거나 증가한다는 것을 확인할 수 있습니다!**

그 이유를 생각해보면 지극히 당연합니다. i가 1이 증가하면 합이 $A_i$ 값만큼 감소하기 때문에 그만큼 더 뒤로 이동할 수 있는 여유 공간이 생기기 때문입니다.

이렇듯 문제에서의 특정 조건에 의해 원하는 구간의 양 끝을 나타내는 2개의 포인터가 한 방향으로만 계속 전진하는 형태의 테크닉을 Two Pointer라고 부릅니다.

Two Pointer를 이용해 i가 1증가했을 때 j는 이전 값에서 시작하여 감소시키지 않고 뻗어나갈 수 있는 최대로 뻗어나가도록 진행을 하면, **i, j 모두 한 방향으로만 진행하기 때문에** 시간복잡도가 $O(N)$ 이 됩니다.

![](https://contents.codetree.ai/problems/1310/images/introductions-b3a510a9-5f6d-462d-a947-b6964b201d89.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-5d6689aa-872b-4462-8133-7fcbcf3c8e2e.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-c71d4f43-4afc-4a39-9ccc-9e758b88ab41.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-bdbb9133-05be-49f6-8132-3606c4076ad0.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-886cb9c0-276a-40ba-bdc1-6e8731798e8f.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-aebe45d3-dfef-4c88-9607-ead21d443ce0.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-d6ebc754-5e2e-41c8-bacc-8d01b6e7777b.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-079a7e8f-a2ff-4d8f-aef8-a2e5d321197c.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-7c04f6e6-cc16-47a7-81f7-58d3e68b25f0.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-5d97439f-f02c-4bfe-80fc-2f6a34ab293b.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-13eeeca7-90b0-40bd-bb02-ec3e9179ee86.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-b20af2b2-6f96-41c7-999a-ffc33e730bdb.png) ![](https://contents.codetree.ai/problems/1310/images/introductions-189b4f40-3e8f-45b7-816b-2b7c4b472587.png)

1 / 13

Two Pointer로 이 문제를 해결한 코드는 다음과 같습니다. 실제 2중 포문으로 작성되어 있지만, i, j 모두 한 반향으로만 진행하기 때문에 시간복잡도가 두 for loop의 곱이 아닌, 합으로 나타내짐에 꼭 유의해야 합니다.

```python
arr = [0, 6, 3, 2, 4, 9, 1]
k = 10
n = 6

# 가능한 구간 중 최대 크기를 구합니다.
ans = 0

# 구간을 잡아봅니다.
sum_val = 0
j = 0
for i in range(1, n + 1):
    # 구간 내 합이 10을 넘지 않을때까지 계속 진행합니다.
    while j + 1 <= n and sum_val + arr[j + 1] <= k:
        sum_val += arr[j + 1]
        j += 1
    
    # 현재 구간 [i, j]는 
    # i를 시작점으로 하는
    # 가장 긴 구간이므로
    # 구간 크기 중 최댓값을 갱신합니다.
    ans = max(ans, j - i + 1)

    # 다음 구간으로 넘어가기 전에
    # arr[i]에 해당하는 값은 구간에서 제외시킵니다.
    sum_val -= arr[i]

# 조건을 만족하는 가장 큰 구간의 크기는
# [3, 2, 4]로 3이 됩니다.
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.