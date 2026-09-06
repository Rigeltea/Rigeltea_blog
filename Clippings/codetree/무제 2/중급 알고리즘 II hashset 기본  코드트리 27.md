---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-sum-of-n-integers-3/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Prefix Sum

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 사각형 내 직사각형 구간 숫자의 합 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
3 * 3 크기의 격자 안에 칸마다 숫자들이 하나씩 주어졌을 때,
다음 직사각형 구간 내 숫자들의 합을 구하는 프로그램을 작성해보세요.

1 2 3
3 6 2
7 5 5

(1, 1) ~ (3, 3) // 1행 1열부터 3행 3열까지 이루어져 있는 직사각형 내 숫자의 합
(1, 2) ~ (3, 2) // 1행 2열부터 3행 2열까지 이루어져 있는 직사각형 내 숫자의 합 
(2, 1) ~ (3, 3) // 2행 1열부터 3행 3열까지 이루어져 있는 직사각형 내 숫자의 합
```

무작정 코드를 작성한다면, 직사각형 구간이 주어질 때마다 각 직사각형 내의 숫자들을 전부 순회하며 합을 구해야 합니다. 직사각형 구간의 최대 크기는 N \* N이므로, 질의의 개수를 Q라 했을 때 총 시간복잡도는 $O(QN^2)$ 이 됩니다.

2차원에서 역시 누적합(prefix sum)을 이용할 수 있습니다. 1차원에서 $S_a - S_{b-1}$ 사용시 $S_0$ 값이 필요했던 것과 같은 이유로 2차원 누적합 배열 이용시에는 되도록 **1 ~ n** 번까지 index를 사용하는 것을 추천드립니다. 또한, 누적합 배열을 처음에 전부 0으로 초기화해놓고 시작하는 것이 좋습니다.

![](https://contents.codetree.ai/problems/2206/images/introductions-94f4307e-d073-4e4d-8f07-4d7675f309e9.png)

이 누적합 배열은 $S_{i,j} = S_{i-1,j} + S_{i,j-1}-S_{i-1,j-1} + A_{i,j}$ 라는 성질을 이용해 채워줄 수 있습니다.

![](https://contents.codetree.ai/problems/2206/images/introductions-53f25eee-15ed-49db-9e78-807deb13714c.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-f5d60cd8-ff06-414d-b873-7acc61669dd6.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-d8368e53-840f-4816-87ea-b2976e602dab.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-5e2c8377-5af5-4b1e-8a61-5fa599499146.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-5a3ee180-6104-41be-aa92-5e5713a6a8ab.png) ![Image](https://contents.codetree.ai/problem_factory/images/21e18586-c5c0-4e30-91a2-aaaec85b4561.webp)

1 / 7

이를 이용하여 순서대로 채워주면 시간복잡도 $O(N^2)$ 에 누적합 배열을 완성할 수 있습니다.

![](https://contents.codetree.ai/problems/2206/images/introductions-8413c8fe-05fc-4c36-bdf4-fb42cfba193e.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-afdca657-77f9-4ad6-9c5d-2d30bb94eadf.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-7c8b66a1-8cea-4b9f-9205-166f5418c46d.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-09f4a427-f9e0-486b-8008-cabf8fbee9f3.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-bded97f2-2ee4-438f-8e86-b82fce51f244.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-aee2d2e6-3c41-49f7-b8d7-9eaf07d9111c.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-78e98724-455f-420e-b049-4ae5c4f294af.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-23aca663-39f8-4401-a74f-21dc5364426a.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-64f3b482-1836-44a7-9831-b22827db1b03.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-e050e390-e86c-46fc-99ca-9473d6116ca4.png)

1 / 10

누적합 배열을 만들기 위해 적용했던 식에서처럼, 구간 `(x1, y1) ~ (x2, y2)` 까지의 합을 누적합 배열을 이용하여 구하기 위한 식은 $S_{x_2, y_2} - S_{x_1 - 1, y_2} - S_{x_2, y_1 - 1} + S_{x_1 - 1, y_1 - 1}$ 이 됩니다.

![](https://contents.codetree.ai/problems/2206/images/introductions-7e64c859-794d-4467-970b-4745c652e110.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-6b0a926b-7f1a-4527-879d-575219b27322.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-0a41a028-b744-4ffe-a6b2-aec22ea679d9.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-f6d93ff7-7bb4-4dd1-8f8f-e34a643e6bb9.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-562e1d04-a0e1-4354-90f7-610fe14c8470.png) ![](https://contents.codetree.ai/problems/2206/images/introductions-0fde1cec-16a7-47a9-8d9a-f3bbb1058585.png)

1 / 6

따라서 누적합 배열을 이용하면 각 질의마다 합을 구하는데 시간이 $O(1)$ 만큼 소요되므로 질의에 필요한 총 시간 복잡도는 $O(Q)$ 가 됩니다.

코드는 다음과 같습니다.

```python
arr = [
    [0, 0, 0, 0],
    [0, 1, 2, 3],
    [0, 3, 6, 2],
    [0, 7, 5, 5]
]
prefix_sum = [
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0]
]

for i in range(1, 4):
    for j in range(1, 4):
        prefix_sum[i][j] = prefix_sum[i - 1][j] + \
                            prefix_sum[i][j - 1] - \
                            prefix_sum[i - 1][j - 1] + \
                            arr[i][j]

# (1, 1) ~ (3, 3) 사이의 합 = 34
print(prefix_sum[3][3] - prefix_sum[0][3] - 
      prefix_sum[3][0] + prefix_sum[0][0])
# (1, 2) ~ (3, 2) 사이의 합 = 13
print(prefix_sum[3][2] - prefix_sum[0][2] - 
      prefix_sum[3][1] + prefix_sum[0][1])
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.