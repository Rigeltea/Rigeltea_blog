---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-find-number-fast/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. 이진탐색

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 이진탐색

업/다운 게임이라는 것을 들어보셨나요? 한 사람이 수를 생각하고, 다른 사람이 수를 예측해서 부르면 그것보다 큰지, 작은지 불러주면서 최대한 빨리 그 수를 맞추는 게임입니다. 많은 사람들이 수를 처음 예측할 땐 범위의 가운데에 해당하는 숫자를 부르고, 그 이후엔 업/다운에 맞춰 특정 구간의 가운데를 부르는 방법으로 수를 추측합니다.

이진탐색의 아이디어도 저것과 동일합니다. 찾아야 하는 수의 범위 중 가운데의 값과 찾고자 하는 값을 비교하여 대소관계에 따라 특정 구간으로 이동하는 것을 반복하는 것입니다.

![](https://contents.codetree.ai/problems/1910/images/introductions-f8629701-4891-43c1-a0e7-82aab576a3f6.png)

업/다운 게임에서 비춰보면, '다운'이라는 말을 들으면 우리는 그 값보다 더 작은 값을 선택해야 하고, '업'을 외쳤다면 더 큰 값을 선택해야 합니다. 이진탐색에서도 저러한 과정을 수행하기 위해선, 당연하게도 대소관계에 따라 실제 찾는 값도 작거나 커져야 하기 때문에 배열에 들어있는 값은 반드시 정렬이 되어있어야 합니다.

![](https://contents.codetree.ai/problems/1910/images/introductions-efe5f35b-2821-48f4-a352-93c3895a1c4d.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-81e5d6f6-68d5-435e-a953-6a7221fd3c9e.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-2415f12d-3a29-49c9-9d4e-2268e6a1e10a.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-bd2c3368-b4d5-44bf-aeae-93c23ee6a3f4.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-2a150a2e-8c4e-4b79-b23d-0d1a61d04eda.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-e48221d4-2e07-490d-956e-723bc4f25add.png) ![](https://contents.codetree.ai/problems/1910/images/introductions-d7765c38-ec75-4525-bc31-639424392652.png)

1 / 7

당연히 우리가 찾는 범위 속 원소의 갯수가 1개로 줄어들 때 까지 계속 탐색을 진행해야 하기 때문에 while문을 통해 조건을 걸고, 이후 중간에 위치한 값의 대소관계에 따라 left와 right의 값을 계속 바꿔가면서 진행하는 것을 볼 수 있습니다. 단, while 조건을 걸 때 `left <= right` 이렇게 등호를 꼭 넣어야 단 하나의 숫자만 남았을 경우에도 올바르게 찾아집니다. 계속 탐색을 반복하며, 그 중 가운데 위치에 해당하는 값인 `arr[mid]` 와 찾으려고 하는 숫자인 `target` 이 일치하면, 해당 위치인 `mid` 를 반환해주게 됩니다. while문이 끝났는데도 불구하고 아직 return이 되지 않았다면, `-1` 을 반환해 원하는 값이 없다는 표시를 해주게 됩니다. 또, `mid = (left + right) / 2` 에서 left + right 값이 홀수라면, mid는 2로 나눈 뒤 버림한 위치에 가게됨에 유의합니다.

왜 left는 mid + 1이고, right는 mid - 1일까요? `arr[mid]` 값이 `target` 값이 아니었으니 mid는 target을 포함할 숫자 범위에서 명확히 제외됩니다. 따라서 mid 위치를 제외한 범위로 left, right를 움직여줘야 함에 유의합니다.

코드는 다음과 같습니다.

```python
n, target = 13, 45
arr = [23, 34, 36, 41, 45, 49, 52, 57, 64, 72, 76, 81, 89]

idx = -1

# 이진탐색을 진행합니다.
left, right = 0, n - 1

while left <= right:
    mid = (left + right) // 2
    if arr[mid] == target: # 찾았다면 해당 index를 반환합니다.
        idx = mid
        break

    if arr[mid] > target:  # 찾으려는 숫자가 더 작다면
        right = mid - 1    # 왼쪽 구간으로 이동해야 합니다.
    else:                  # 찾으려는 숫자가 더 크다면
        left = mid + 1     # 오른쪽 구간으로 이동해야 합니다.

print(idx) # 45가 있는 인덱스인 4가 답이 됩니다.
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.