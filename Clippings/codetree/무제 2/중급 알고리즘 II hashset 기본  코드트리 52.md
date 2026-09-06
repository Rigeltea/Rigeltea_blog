---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-number-of-integers/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. 이진탐색

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Lower bound, Upper bound

## Lower Bound

만약 내가 찾는 값 target이 배열에 여러 개 있다면, 이진탐색을 돌렸을 때 어떤 위치가 나오게 될지는 아무도 모릅니다. 이런 경우에 보통 사용하는 것이 Lower Bound 입니다. Python에서는 `bisect_left` 라는 이름으로 더 알려져 있습니다.

![](https://contents.codetree.ai/problems/1928/images/introductions-63f48fa1-0ae2-4fe0-82ba-989229450516.png)

**Lower Bound는 원하는 값 target 이상의 값이 최초로 나오는 위치를 의미합니다.** 이는 바꿔말해 target보다 같거나 큰 원소의 위치들 중 가장 작은 값을 출력해야 한다는 것입니다. 따라서 작은 값을 구하기 위해 `min_idx` 라는 변수를 활용해 초기값으로 답이 될 수 없는 최댓값인 `n` 을 넣어놓고 문제를 해결합니다. 다음과 같은 형태가 될 것입니다.

```python
def lower_bound(target):
    left = 0
    right = n - 1
    min_idx = n

    while left <= right:
        mid = (left + right) // 2
        if (1):
            (2)
        else:
            (3)
    
    return min_idx
```

이때, min\_idx 값이 갱신되는 순간이 언제인지를 생각합니다. min\_idx는 정의상 **arr\[mid\]가 target보다 같거나 큰 경우** 에 대해 가능한 mid 값들 중 최솟값이 되어야 합니다. 따라서 (1) 위치에 `arr[mid] >= target` 조건을 걸어줍니다. 왼쪽에 조건을 만족하는 mid값이 더 있을 수 있으므로 right값을 움직여줘야 하며, 이 경우 min\_idx를 현재까지의 최솟값인 min\_idx와 mid를 비교하여 둘 중 더 작은 값으로 넣어줘야 합니다. 조건을 만족하지 않는 경우에는 left값을 움직여 주면 됩니다. 따라서 Lower Bound 코드는 다음과 같이 작성이 가능합니다.

```python
def lower_bound(target):
    left = 0                             # 첫 번째 원소의 위치로 설정합니다.
    right = n - 1                        # 마지막 원소의 위치로 설정합니다.
    min_idx = n                          # 최소이므로, 답이 될 수 있는 값보다 더 큰 값으로 설정합니다.

    while left <= right:                 # [left, right]가 유효한 구간이면 계속 수행합니다.
        mid = (left + right) // 2        # 가운데 위치를 선택합니다.
        if arr[mid] >= target:           # 만약에 선택한 원소가 target보다 같거나 크다면 
            min_idx = min(min_idx, mid)  # 같거나 큰 값들의 위치 중 최솟값을 계속 갱신해줍니다.
            right = mid - 1              # 왼쪽에 조건을 만족하는 숫자가 더 있을 가능성 때문에 right를 바꿔줍니다.
        else:
            left = mid + 1               # 작은 경우라면 left를 바꿔줍니다.
    
    return min_idx                       # 조건을 만족하는 최소 index 값을 반환합니다.
```

## Upper Bound

Upper Bound는 원하는 값 target을 초과하는 값이 최초로 나오는 위치를 의미합니다. Python에서는 `bisect_right` 라는 이름으로 더 알려져 있습니다.

![](https://contents.codetree.ai/problems/1928/images/introductions-7f0c3bb0-0d04-49d8-bc27-3ec9b10b5b33.png)

Lower Bound 코드에서 등호만 제외하면, Upper Bound가 구해지는 코드가 됩니다.

```python
def upper_bound(target):
    left = 0                             # 첫 번째 원소의 위치로 설정합니다.
    right = n - 1                        # 마지막 원소의 위치로 설정합니다.
    min_idx = n                          # 최소이므로, 답이 될 수 있는 값보다 더 큰 값으로 설정합니다.

    while left <= right:                 # [left, right]가 유효한 구간이면 계속 수행합니다.
        mid = (left + right) // 2        # 가운데 위치를 선택합니다.
        if arr[mid] > target:            # 만약에 선택한 원소가 target보다 크다면 
            min_idx = min(min_idx, mid)  # 큰 값들의 위치 중 최솟값을 계속 갱신해줍니다.
            right = mid - 1              # 왼쪽에 조건을 만족하는 숫자가 더 있을 가능성 때문에 right를 바꿔줍니다.
        else:
            left = mid + 1               # 같거나 작은 경우라면 left를 바꿔줍니다.
    
    return min_idx                       # 조건을 만족하는 최소 index 값을 반환합니다.
```

## Lower/Upper bound

Lower bound와 upper bound의 성질을 잘 이해하면, 배열 내 특정 값의 개수를 쉽게 구할 수 있습니다. 특정 값의 개수는 upper bound에서 lower bound를 뺀 값과 같으며, 해당 값이 배열에 존재하지 않는다면 두 값이 같아지므로 차이는 0이 됩니다.

예를 들어, 아래 그림에서 $45$ 의 개수를 구하고 싶다면, `upper_bound(45) = 6` 에서 `lower_bound(45) = 3` 을 빼면 $3$ 이 되므로 45가 3개 있음을 알 수 있습니다.

![Image](https://contents.codetree.ai/problem_factory/images/1024d8d7-46aa-45d1-a570-c8884eb6d9b9.webp)

## Custom Bound

target보다 같거나 작은 숫자들이 있는 위치 중 가장 큰 위치를 구하는 함수는 어떻게 작성해 볼 수 있을까요?

![](https://contents.codetree.ai/problems/1928/images/introductions-88cd4721-59d9-4e57-910b-8d09c3f1dd1e.png)

**Custom Bound는 원하는 값 target 이하의 값이 마지막으로 나오는 위치를 의미합니다.** 이는 바꿔말해 target보다 같거나 작은 원소의 위치들 중 가장 큰 값을 출력해야 한다는 것입니다. 따라서 큰 값을 구하기 위해 `max_idx` 라는 변수를 활용해 초기값으로 답이 될 수 없는 최솟값인 `-1` 을 넣어놓고 문제를 해결합니다. 다음과 같은 형태가 될 것입니다.

```python
def custom_bound(target):
    left = 0          
    right = n - 1            
    max_idx = -1          

    while left <= right:            
        mid = (left + right) // 2     
        if (1):
            (2)      
        else:
            (3)
    
    return max_idx
```

이때, max\_idx 값이 갱신되는 순간이 언제인지를 생각합니다. max\_idx는 정의상 **arr\[mid\]가 target보다 같거나 작은 경우** 에 대해 가능한 mid 값들 중 최댓값이 되어야 합니다. 따라서 (1) 위치에 `arr[mid] <= target` 조건을 걸어줍니다. 오른쪽에 조건을 만족하는 mid값이 더 있을 수 있으므로 left값을 움직여줘야 하며, 이 경우 max\_idx를 현재까지의 최댓값인 max\_idx와 mid를 비교하여 둘 중 더 큰 값으로 넣어줘야 합니다. 조건을 만족하지 않는 경우에는 right값을 움직여 주면 됩니다. 따라서 Custom Bound 코드는 다음과 같이 작성이 가능합니다.

```python
def custom_bound(target):
    left = 0                             # 첫 번째 원소의 위치로 설정합니다.
    right = n - 1                        # 마지막 원소의 위치로 설정합니다.
    max_idx = -1                         # 최대이므로, 답이 될 수 있는 값보다 더 작은 값으로 설정합니다.

    while left <= right:                 # [left, right]가 유효한 구간이면 계속 수행합니다.
        mid = (left + right) // 2        # 가운데 위치를 선택합니다.
        if arr[mid] <= target:           # 만약에 선택한 원소가 target보다 같거나 작다면 
            max_idx = max(max_idx, mid)  # 같거나 작은 값들의 위치 중 최댓값을 계속 갱신해줍니다.
            left = mid + 1               # 오른쪽에 조건을 만족하는 숫자가 더 있을 가능성 때문에 left를 바꿔줍니다.
        else:
            right = mid - 1              # 값이 더 큰 경우라면 right를 바꿔줍니다.
    
    return max_idx                       # 조건을 만족하는 최대 index 값을 반환합니다.
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.