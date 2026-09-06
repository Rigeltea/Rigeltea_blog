---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-taking-a-taxi-in-the-middle-of-the-marathon/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. LR Technique

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## LR Technique

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, 6, 7, 5, 2] 와 같이 숫자들이 주어졌을 때,
다음 질의에 대해 답하는 프로그램을 작성해보세요.

단, 질의마다 하나의 숫자가 주어지며 
해당 번째 숫자를 제외한
다른 숫자들에 대해 인접한 숫자간의 차이의 합을 구해야 합니다.

예를 들어 질의로 5가 주어졌다면
5번째 숫자인 7을 제외한 다른 숫자들을 나열하면
[3, 6, 2, 6, 5, 2]가 되므로
인접한 숫자간의 차이의 합은
|3 - 6| + |6 - 2| + |2 - 6| + |6 - 5| + |5 - 2| = 15가 됩니다.

이때 주어지는 숫자는 1초과 N 미만임을 가정해도 좋습니다.
```

무작정 코드를 작성한다면, 숫자가 주어질 때마다 남은 숫자 N - 1개를 순회해야 하므로 $O(N)$ 시간이 소요됩니다. 즉, 질의의 개수를 Q라 했을 때 총 시간복잡도는 $O(QN)$ 이 됩니다.

이를 개선시킬 수 있습니다.

4번째 숫자를 제외했을 경우 답을 구하는 과정을 그려보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/778/images/introductions-eb6f2ca1-5006-4ef7-9da4-274655fe53bf.png)

5번째 숫자를 제외했을 경우 답을 구하는 과정을 그려보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/778/images/introductions-5d9ccae4-cdec-4462-bf62-4f23fed7c372.png)

중복되는 계산이 보이시나요?

`[1, 3]` 번까지는 동일하게 인접한 숫자간의 계산을 반복하는 모습을 볼 수 있습니다.

이때, 이런 생각을 한 번 해볼 수 있습니다. 만약 $L$ 배열이 있어 $L_i$ = 1번부터 i번까지 인접한 숫자간의 쌍의 합이 전부 구해져 있고, $R$ 배열이 있어 $R_i$ = i번 부터 N번까지 인접한 숫자간의 쌍의 합이 전부 구해져 있다면, i번째 숫자를 제외했을 때 인접한 숫자간의 합을 빠르게 구할 수 있지 않을까요?

![](https://contents.codetree.ai/problems/778/images/introductions-a51f6c3a-6ace-443c-8211-4929f1c3042c.png)

가능합니다. 예를 들어 4번째 숫자를 제외하는 경우를 생각해보겠습니다.

![](https://contents.codetree.ai/problems/778/images/introductions-8c1805cc-448b-4af7-8954-e1d6dadb150f.png)

L 배열이 이미 구해져있다면, 1번째부터 3번째 숫자까지 인접한 숫자간의 합은 $L_3$ 에 들어있으므로 이를 이용하면 됩니다.

![](https://contents.codetree.ai/problems/778/images/introductions-790d803a-21d1-451b-aada-0f3873531c98.png)

R 배열 역시 이미 구해져 있으므로, 5번째부터 7번째 숫자까지 인접한 숫자간의 합은 $R_5$ 에 들어있으므로 이를 이용하면 됩니다.

![](https://contents.codetree.ai/problems/778/images/introductions-56f4c2da-a935-4ed8-ad21-4412441e84cc.png)

이제 남은 곳은 4번째 숫자가 사라졌기에 서로 인접해진 3번째, 5번째 숫자간의 차이의 합 입니다. 이는 $|A_5 - A_3|$ 으로 바로 계산이 가능합니다.

![](https://contents.codetree.ai/problems/778/images/introductions-ad5293a1-8283-4a0f-9143-c2f060c31b02.png)

이를 일반화하면 i번째 숫자를 제외했을 때 인접한 숫자간의 합을 $L_{i-1} + R_{i+1} + |A_{i+1} - A_{i-1}|$ 라는 식으로 바로 나타낼 수 있습니다. $L_{i-1}$ 은 1번부터 i - 1번째까지 인접한 숫자간의 합을, $R_{i + 1}$ 은 i + 1번부터 N번째까지 인접한 숫자간의 합을 담고 있기 때문에, i - 1번째와 i + 1번째 사이의 차이인 $|A_{i + 1}-A_{i - 1}|$ 값만 더 더해주면 됩니다.

![](https://contents.codetree.ai/problems/778/images/introductions-1853694f-4d70-4d2a-9469-cf84ca845391.png)

따라서 L, R 배열이 있다면 질의마다 답을 구하는 시간복잡도는 $O(1)$ 이 됩니다.

L 배열은 다음과 같이 $L_1$ 에는 0을 넣어주고, 정의상 $L_i = L_{i-1} + |A_i - A_{i-1}|$ 임을 이용하면 $L_2$ 부터 순서대로 채워줄 수 있기 때문에 $O(N)$ 에 모든 값을 채울 수 있게 됩니다.

![](https://contents.codetree.ai/problems/778/images/introductions-2f2f68ac-b75b-4b89-b0a2-30a01a765166.png) ![](https://contents.codetree.ai/problems/778/images/introductions-eb993924-513b-404a-9aab-fec06b7cf23e.png) ![](https://contents.codetree.ai/problems/778/images/introductions-062ae6d4-6623-4bca-8d0d-ebb29be59861.png) ![](https://contents.codetree.ai/problems/778/images/introductions-966cf66d-bc47-47af-93a8-53f4d92c440a.png) ![](https://contents.codetree.ai/problems/778/images/introductions-519589ce-a136-43e1-b244-8bcaea54021b.png) ![](https://contents.codetree.ai/problems/778/images/introductions-d296515c-12db-4d16-8a04-afd11e8df803.png) ![](https://contents.codetree.ai/problems/778/images/introductions-2636f69d-cbaf-460b-929b-1c946e6743d9.png) ![](https://contents.codetree.ai/problems/778/images/introductions-ab2aafdd-fbcc-4eec-971f-1e48b2977eb8.png)

1 / 8

R 배열 역시 마찬가지로 처음 $R_N$ 에 0을 넣어주고, 정의상 $R_i = R_{i+1} + |A_{i+1} - A_i|$ 임을 이용하면 $R_{N-1}$ 부터 순서대로 채워줄 수 있기 때문에 $O(N)$ 에 모든 값을 채울 수 있게 됩니다.

![](https://contents.codetree.ai/problems/778/images/introductions-f162ce29-dedd-43b7-bc8d-7b10b717c837.png) ![](https://contents.codetree.ai/problems/778/images/introductions-3603da33-3127-4bb9-8a90-ff9f2d81fa9b.png) ![](https://contents.codetree.ai/problems/778/images/introductions-a7fe348c-d68c-44c8-a23e-ae82429a618c.png) ![](https://contents.codetree.ai/problems/778/images/introductions-382137b3-c250-4457-ba48-3be87dede7f8.png) ![](https://contents.codetree.ai/problems/778/images/introductions-8594d69c-a8d2-454a-b563-84585f50d639.png) ![](https://contents.codetree.ai/problems/778/images/introductions-cb42a742-6a7a-4b08-8208-c18102e7b73d.png) ![](https://contents.codetree.ai/problems/778/images/introductions-0d2e0223-01d9-444f-a1ae-f1ab22954250.png) ![](https://contents.codetree.ai/problems/778/images/introductions-bbf8660c-9a48-4c66-8f52-42e530437a20.png)

1 / 8

이렇듯 L, R 배열만 $O(N)$ 에 미리 채우게 되면, 질의마다 시간복잡도 $O(1)$ 에 원하는 답을 구할 수 있게 되므로 총 Q개의 질의에 대한 시간복잡도는 $O(N + Q)$ 가 됩니다. 이렇게 문제에서 원하는 정답을 미리 L, R 배열을 이용하여 구현하는 방식을 LR Technique이라 부릅니다.

코드는 다음과 같습니다.

```python
arr = [0, 3, 6, 2, 6, 7, 5, 2]
L = [0] * 8
R = [0] * 8
n = 7

# L 배열을 채워줍니다.
L[1] = 0
for i in range(2, n + 1):
    L[i] = L[i - 1] + abs(arr[i] - arr[i - 1])

# R 배열을 채워줍니다.
R[n] = 0
for i in range(n - 1, 0, -1):
    R[i] = R[i + 1] + abs(arr[i + 1] - arr[i])

# 4번째 숫자를 제외했을 때의 답 = 17
print(L[3] + R[5] + abs(arr[5] - arr[3]))
# 5번째 숫자를 제외했을 때의 답 = 15
print(L[4] + R[6] + abs(arr[6] - arr[4]))
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.