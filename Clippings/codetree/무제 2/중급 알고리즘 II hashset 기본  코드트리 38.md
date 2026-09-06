---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-section-with-maximum-overlap/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. +1-1 technique

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## +1-1 Technique

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
1차 수직선 상에 n개의 선분이 주어졌을 때, 
x = k 직선과 만나는 서로 다른 선분의 수는 몇 개인지를 판단하는 
프로그램을 작성해보세요.
단, 주어지는 x 좌표는 모두 다름을 가정해도 좋습니다.
```

예로, 다음 그림에서의 답은 2가 됩니다.

![](https://contents.codetree.ai/problems/1757/images/introductions-ecd582c6-d771-4d31-8515-14bd97eab196.png)

눈으로 봤을 때는 지극히 당연히 2개라는 것을 알 수 있지만, 이를 컴퓨터가 계산하기 쉽게 나타내기 위해서는 어떻게 해야 할까요?

바로 선분마다 시작점에는 **+1**, 끝나는 지점에는 **\-1** 을 적은 뒤, 빨간선 앞에 있는 점들에 적혀있는 숫자들을 전부 더해주면 됩니다. 이 의미는 곧 앞에 시작, 끝 지점이 전부 다 있는 선분들은 0으로 처리하고, 단 시작점만 나온 선분들에 대해서는 +1을 진행한다는 뜻입니다.

![](https://contents.codetree.ai/problems/1757/images/introductions-d358644c-94d3-412b-ae13-00287a5d2c2b.png)

이 점을 활용하면 주어지는 모든 선분 N개를 각각 2개의 시작점, 끝점으로 구분하여 총 2N개의 점으로 나눠 이를 x좌표 순으로 오름차순 정렬한 뒤, x = k보다 커지기 직전까지의 숫자를 전부 더하는 식으로 진행해볼 수 있습니다.

![](https://contents.codetree.ai/problems/1757/images/introductions-8a8204d2-f2c4-40d6-a580-7e9a9887f232.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-9977397b-fae8-4d4f-ab29-bb2c16af2f92.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-7dc5013f-bf00-4a57-815e-fb6c25517a96.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-4c383ff5-8d28-485b-8473-9e8971fb186d.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-ff92114f-fe80-4744-b6fe-eedf910c2019.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-5456c572-ff48-4650-9006-80d547a5c535.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-50a9707f-dd20-474b-be3d-646679c65419.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-e931ec41-3ea6-4794-a391-bd2b9cce6e89.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-236b3bd8-7688-416e-839b-a6402b0a2ff3.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-0900a7ef-2633-4133-ad0a-2f99406e0c69.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-34bc21ee-d1dc-49ab-967c-7a29eda9cfba.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-b50a2a16-0459-4b0b-83ab-d7f8100016ab.png)

1 / 12

이렇듯 N개의 선분을 2개의 시작, 끝 정점으로 나눠 각각 +1, -1 가중치를 줘서 x가 증가하는 순서대로 정렬하는 방법을 +1 -1 Technique이라 부릅니다.

### 구현 1.

+1-1 Technique의 경우 좌표의 범위가 작을 때는 배열을 이용하여 해결할 수 있습니다. 배열을 하나 만들어, 주어진 각 선분의 양 끝점 중 시작점에 해당하는 위치에 +1, 끝점에 해당하는 위치에 -1을 더해주는 방식으로 진행하면 됩니다. 이때 배열의 크기는 최대 좌표의 범위 만큼 잡아야 하며, 이후 각 칸을 x = 1부터 최대 위치까지 순서대로 순회하며 적혀있는 숫자를 더하는 식으로 진행하면 됩니다.

그 과정은 다음과 같습니다.

![](https://contents.codetree.ai/problems/1757/images/introductions-ff3a13b0-dc1a-46f9-9c3c-3b064699d444.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-d78c9dff-d5a5-4fe7-b566-f653ae20267f.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-7842bc54-ca2e-460a-a216-70f60df8921c.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-ea6b2f5c-5d76-4bc1-a32a-fec621797b80.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-9a19f9f1-9559-4b71-96e2-58ccff52f38c.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-cb690a11-9a12-4d20-b727-2510d522b575.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-af29c55a-338b-41f5-ae52-173a67fb583e.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-aed7e789-7bbc-4a1d-a9a8-d6d98ec95b40.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-eb550ae0-5cad-41ee-8e68-4da60e74dbf0.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-c6f7dcb8-f1a7-4b1f-ac45-588c790550d7.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-431bb8bc-f7cd-40aa-96cd-7dcc376676f9.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-ce38058f-5ce3-46e6-b4aa-33d30cfb7518.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-0682b84d-1108-44b0-8648-eec65e9f47e4.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-12143006-f5a5-4229-aef5-844181b019fe.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-94148d75-6f6f-46e1-80cc-3d892b369bff.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-10892667-cdf7-4639-99b5-9ae6b1f2a4f9.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-e93e94e7-d3cd-4964-9ca8-9e5a9b467a8a.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-e78da200-fef6-48f9-9ca2-e5b7ff1b73a5.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-47396a3f-0094-4409-afd8-994b12bf0383.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-8b66c22f-17be-452a-96fc-a304dfe3b34f.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-d31801ee-7008-4aaa-9d4c-ef347109d591.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-777dd1da-de71-4e09-9f53-abf5fd5498bf.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-6a04282e-568e-4399-874a-59eb4665e603.png)

1 / 23

코드는 다음과 같습니다.

```python
segments = [
    (1, 5), (4, 7), (3, 6), (5, 10), 
    (9, 13), (8, 15), (12, 16)
]
n = 7
k = 11

# 주어진 좌표의 범위가 작을 때에는
# 배열을 이용하여 직접 각 칸에
# +1 -1을 진행해도 무방합니다.
checked = [0] * 21

for x1, x2 in segments:
    checked[x1] += 1
    checked[x2] -= 1

# x = k 전까지
# 각 위치에 적혀있는 숫자들의 합을 구해줍니다.
sum_val = 0
for i in range(1, k):
    sum_val += checked[i]

# x = k에 겹쳐져 있는 선분의 수 = 2
print(sum_val)
```

### 구현 2.

+1-1 Technique 이용시 좌표의 범위가 클 경우에는 직접 양쪽 끝점을 정렬을 이용해야 합니다. 선분 N개를 각각 2개의 시작점, 끝점으로 구분하여 총 2N개의 점으로 나눠 이를 x좌표 순으로 오름차순 정렬이 되도록 하면 됩니다.

이 과정은 위에서 처음 소개드린 과정과 동일합니다.

![](https://contents.codetree.ai/problems/1757/images/introductions-a6631c3c-df68-42f0-a04e-1e4792346309.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-3e8b119a-c1ff-48fd-9f23-7b5b201f9f11.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-0a626b2d-38fe-47b3-b878-deae57b97185.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-ac3a2dea-22fb-41c8-8c17-d3a57a572f83.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-6e286093-4d9c-4877-b659-0485cfb926ba.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-b186b16e-92c1-4b75-b9d4-a8e6f1a16a8b.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-910c5a56-4557-40d5-823d-c3134b0764dc.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-10ed1311-6eb7-46ad-bc6c-f6c5e7e24607.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-f5f5eacb-8f18-406e-87b7-cdfbf2062750.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-be53b7ef-9c48-4ba3-8ab5-4bc73d8c574e.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-74453174-f53d-40b8-b347-d4937919a6cb.png) ![](https://contents.codetree.ai/problems/1757/images/introductions-b438a5b9-98e1-4584-bd34-cddac0dea090.png)

1 / 12

코드는 다음과 같습니다.

```python
segments = [
    (1, 5), (4, 7), (3, 6), (5, 10), 
    (9, 13), (8, 15), (12, 16)
]
n = 7
k = 11

# 주어진 좌표의 범위가 큰 경우에는
# 각 선분을 두 지점으로 나눠서
# +1, -1로 담은 뒤,
# 정렬해줍니다.
points = []
for x1, x2 in segments:
    points.append((x1, +1)) # 시작점
    points.append((x2, -1)) # 끝점

# 정렬을 진행합니다.
points.sort()

# x = k 전까지
# 각 위치에 적혀있는 숫자들의 합을 구해줍니다.
sum_val = 0
for x, v in points:
    # x가 k 이상이 되면 종료합니다.
    if x >= k:
        break

    # 적혀있는 가중치를 전부 더해줍니다.
    sum_val += v

# x = k에 겹쳐져 있는 선분의 수 = 2
print(sum_val)
```

## Side Note

+1-1 Technique를 이용하면 N개의 선분이 주어졌을 때, 가장 많이 겹치는 지점에서 총 몇 개의 선분이 겹쳐있는지도 쉽게 구할 수 있습니다. x = k에 대해서만 진행하는 것이 아닌, 모든 시작, 끝점에 대해 x 기준 오름차순으로 순서대로 보면서 각 순간마다 sum 값을 계산하고, 그 중 최댓값을 계속 갱신해준다면 이 값이 바로 가장 많이 겹치는 지점에서의 겹치는 횟수가 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.