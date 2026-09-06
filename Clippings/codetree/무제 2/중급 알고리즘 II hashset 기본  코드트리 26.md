---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-sum-of-n-integers-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Prefix Sum

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 구간 내 숫자의 합 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, 6, 7, 7, 2] 와 같이 숫자들이 주어졌을 때,
다음 구간 내 숫자들의 합을 구하는 프로그램을 작성해보세요.

[2, 5] // 2번째 원소부터 5번째 원소까지의 합
[3, 6] // 3번째 원소부터 6번째 원소까지의 합
[1, 7] // 1번째 원소부터 7번째 원소까지의 합
```

무작정 코드를 작성한다면, 구간이 주어질 때마다 각 구간 내의 숫자들을 전부 순회하며 합을 구해야 합니다. 구간의 최대 크기는 N이므로, 질의의 개수를 Q라 했을 때 총 시간복잡도는 $O(QN)$ 이 됩니다.

이를 개선시킬 수 있습니다.

먼저 다음과 같이 누적합(prefix sum) 배열을 만들어 줍니다. 누적합 배열은, 처음부터 각 위치까지의 숫자를 전부 더한 배열입니다.

![](https://contents.codetree.ai/problems/1322/images/introductions-d564fdf0-7ab6-4f7d-9a02-91f81d58959c.png)

이러한 누적합 배열을 만드는 데에는 시간이 $O(N)$ 만큼 소요됩니다. S1부터 시작하여 순서대로 $S_i = S_{i-1} + A_i$ 를 이용하여 순차적으로 채워주면 되기 때문입니다.

![](https://contents.codetree.ai/problems/1322/images/introductions-7d90be54-d732-4150-8fa4-3f56ffe156f1.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-a76bfc7d-1b06-4d38-baab-547948a6240d.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-ae8fe4b9-15d1-417e-a60f-cd766c404f21.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-ee6492c4-1bd8-4981-8b04-6fcdc8d66763.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-500c84e8-133f-41db-b229-767f3ec4a9aa.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-b16cab70-2473-4b6d-864b-ab0d6580ec8f.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-5c273d46-cafe-4d07-b356-22b2fb629f17.png) ![](https://contents.codetree.ai/problems/1322/images/introductions-8bac11ae-42f3-42ea-ba10-f04927fc0554.png)

1 / 8

이제 만약 구간 `[a, b]` 사이에 있는 숫자들을 전부 더하려고 한다면 이전에는 직접 하나하나 값을 더해줬었습니다.  
하지만 누적합 배열 $S$ 를 이용하면 $A_a + A_{a + 1} + ... + A_b$ 는 $S_b - S_{a-1}$ 과 같기 때문에 $O(1)$ 시간에 답을 구할 수가 있게 됩니다.

![](https://contents.codetree.ai/problems/1322/images/introductions-b2eaa2e3-9fdc-4664-a456-e1156e96ca13.png)

이때 `[1, 5]` 구간 내 숫자의 합을 구하면 어떻게 될까요?

식대로면 $S_5 - S_0$ 이 올바른 답을 구해줘야 하므로 $S_0$ 이 0이어야만 올바른 답을 주게 됩니다. 이처럼 누적합을 이용할 때 1~n까지 인덱스를 사용한다면, $S_0$ 에 꼭 값 0을 넣어주셔야만 합니다.

![](https://contents.codetree.ai/problems/1322/images/introductions-32830db1-6740-48ec-b7e4-bd1eef46f20f.png)

코드와 함께 보면 다음과 같습니다.

```python
arr = [0, 3, 6, 2, 6, 7, 7, 2]
prefix_sum = [0] * 8

prefix_sum[0] = 0
for i in range(1, 8):
    prefix_sum[i] = prefix_sum[i - 1] + arr[i]
    
# 구간 [2, 5]까지 합 = 21
print(prefix_sum[5] - prefix_sum[1])
# 구간 [1, 5]까지 합 = 24
print(prefix_sum[5] - prefix_sum[0])
```

## Side Note

그렇다면 0 ~ n - 1까지 인덱스를 사용하는 경우에는 누적합을 이용하지 못하는 걸까요?

꼭 그렇지만은 않습니다. $A_a + A_{a + 1} + ... + A_b$ 는 실은 $S_b - S_{a} + A_a$ 라는 식으로도 나타낼 수 있기 때문에 $S_{a-1}$ 이 없어져 음수 인덱스를 참조하지 않고도 원하는 답을 얻을 수 있게 됩니다.

코드는 다음과 같습니다.

```python
arr = [3, 6, 2, 6, 7, 7, 2]
prefix_sum = [0] * 7

prefix_sum[0] = arr[0]
for i in range(1, 7):
    prefix_sum[i] = prefix_sum[i - 1] + arr[i]
    
# 구간 [1, 4]까지 합 = 21
print(prefix_sum[4] - prefix_sum[1] + arr[1])
# 구간 [0, 4]까지 합 = 24
print(prefix_sum[4] - prefix_sum[0] + arr[0])
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.