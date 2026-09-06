---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-pair-parentheses/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. 전처리

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Preprocessing

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[8, 2, 6, 7, 5, 3] 와 같이 숫자들이 주어졌을 때,
특정 위치를 적절하게 선택하여
해당 위치에 놓여있는 숫자와 그 숫자를 포함하여 뒤에 놓여있는 숫자들 중 최솟값을
곱한 값이 최대가 되도록 하는 프로그램을 작성해보세요.

만약 위의 예에서 1번째 위치를 골랐다면,
1번째 위치에는 숫자 8이 있고, 해당 위치에서부터 맨 뒤에 있는 숫자까지 중 최솟값은 2이므로
8 * 2 = 16이 됩니다.

하지만 만약 4번째 숫자를 골랐다면,
4번째 위치에는 숫자 7이 있고, 해당 위치에서부터 맨 뒤에 있는 숫자까지 중 최솟값은 3이므로
7 * 3 = 21로 최대가 됩니다.
```

무작정 코드를 작성한다면, 각 위치를 한번 씩 잡아보면서 그 뒤에 있는 숫자를 전부 보며 최솟값을 구해 곱해보면 되므로 위치 잡는데 $O(N)$, 뒤에 있는 숫자를 보는데 최악에 $O(N)$ 이 소요되므로 총 시간복잡도는 $O(N^2)$ 이 됩니다.

이때 만약 $R$ 이라는 배열이 있어, $R_i$ = i번째부터 N번째까지 놓여있는 숫자들 중 최솟값을 미리 다 구해놓았다면, 각 위치를 잡아보면서 바로 해당 숫자 $A_i$ 와 $R_i$ 를 곱한 값 중 최댓값을 구하면 되므로 $O(N)$ 에 답을 구할 수 있었을 것입니다.

![](https://contents.codetree.ai/problems/634/images/introductions-334bb672-d080-4f12-bb12-5ea5bd38eca2.png) ![](https://contents.codetree.ai/problems/634/images/introductions-8d56e63c-f2fd-41e2-ae1f-c851ade721b2.png) ![](https://contents.codetree.ai/problems/634/images/introductions-b43abc14-ea84-4d51-988a-1de49eff39dc.png) ![](https://contents.codetree.ai/problems/634/images/introductions-ceb48188-0f97-4140-b716-82248a4dff7c.png) ![](https://contents.codetree.ai/problems/634/images/introductions-776b1ed9-a187-43df-9882-4a1f665f1548.png) ![](https://contents.codetree.ai/problems/634/images/introductions-24d55a9c-cb5b-4b6f-8431-5e1f424ded81.png) ![](https://contents.codetree.ai/problems/634/images/introductions-59a851eb-9a80-4f0f-a5a4-b85beced6489.png) ![](https://contents.codetree.ai/problems/634/images/introductions-47b228ef-f60c-482c-98f5-44531dc3515e.png)

1 / 8

$R$ 배열은 $R_N$ 은 $A_N$ 과 같으니 처음에 넣어주고, N - 1번째부터 1번째까지 뒤에서부터 앞으로 오며 $R_i = min(R_{i+1}, A_i)$ 식을 적용하여 채워주면 $O(N)$ 에 모든 값을 채워줄 수 있게 됩니다.

![](https://contents.codetree.ai/problems/634/images/introductions-9f4a2f00-3691-40a2-9495-697c43910be2.png) ![](https://contents.codetree.ai/problems/634/images/introductions-29bd878d-d301-410c-8bdb-e3bf3f331986.png) ![](https://contents.codetree.ai/problems/634/images/introductions-4337af8d-d594-4fc7-a2a4-43f6d8324fcd.png) ![](https://contents.codetree.ai/problems/634/images/introductions-954f21d8-81ae-4e71-9b47-f42a6cdce6c6.png) ![](https://contents.codetree.ai/problems/634/images/introductions-e4e7e883-3356-4987-bae7-e59d3ab58ca3.png) ![](https://contents.codetree.ai/problems/634/images/introductions-6f07a30e-1158-44b6-9279-d53b2368138b.png) ![](https://contents.codetree.ai/problems/634/images/introductions-e0cfc246-fd9d-4cda-9938-c5e88380396b.png) ![](https://contents.codetree.ai/problems/634/images/introductions-0f561368-5242-4adc-b2dd-2710c94cf4f9.png)

1 / 8

따라서 이 문제의 총 시간복잡도는 처음 Preprocessing 작업에 $O(N)$, 답을 구하는 데 $O(N)$ 이 소요되므로 총 $O(N)$ 에 해결이 가능합니다.  
이렇듯 미리 원하는 값을 배열에 담아 놓은 뒤, 이를 이용하여 원하는 작업을 수행하는 방법을 Preprocessing(전처리) 라고 부릅니다.

코드는 다음과 같습니다.

```python
import sys

INT_MIN = -sys.maxsize

arr = [0, 8, 2, 6, 7, 5, 3]
R = [0] * 7
n = 6

# R 배열을 채워줍니다.
R[n] = arr[n]
for i in range(n - 1, 0, -1):
    R[i] = min(R[i + 1], arr[i])

# 답을 구해줍니다.
ans = INT_MIN
for i in range(1, n + 1):
    ans = max(ans, arr[i] * R[i])

# 가능한 최댓값 = 21
print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.