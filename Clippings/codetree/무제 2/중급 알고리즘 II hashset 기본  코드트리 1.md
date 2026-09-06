---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-data-comparison/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. HashSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 존재 여부를 빠르게 판단하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```python
2개의 리스트 arr1 = [1, 2, 5, 3, 2], arr2 = [5, 5, 2, 3, 1, 2, 2, 5]가 
주어졌을 때, 두 리스트를 이루고 있는 원소의 종류가 정확히 동일한지 판단해보세요.
```

이 문제를 arr1에 있는 모든 원소들이 전부 arr2에 하나 이상씩 존재하며,  
arr2에 있는 모든 원소들 역시 전부 arr1에 하나 이상씩 존재하는지를 확인하는 문제로 생각해볼 수 있습니다.

arr1를 이루고 있는 구성 성분을 set1이라 한다면, 이는 다음과 같이 구현이 가능합니다.

```python
arr1 = [1, 2, 5, 3, 2]
set1 = set(arr1)
```

arr2를 이루고 있는 구성 성분을 set2이라 한다면, 이 역시 비슷하게 다음과 같이 구현이 가능합니다.

```python
arr2 = [5, 5, 2, 3, 1, 2, 2, 5]
set2 = set(arr2)
```

그렇다면 이제 arr1에 있는 모든 원소들이 전부 arr2에 하나 이상씩 존재하는지를 set2를 이용해 $O(N1)$ 에 구현이 가능해집니다.

```python
not_exist = False
for elem1 in arr1:
    if elem1 not in set2:
        not_exist = True
```

마찬가지 방법으로 arr2에 있는 모든 원소들이 전부 arr1에 하나 이상씩 존재하는지를 set1를 이용해 $O(N2)$ 에 구현이 가능합니다.

```python
not_exist = False
for elem2 in arr2:
    if elem2 not in set1:
        not_exist = True
```

최종 답은 not\_exist가 최종적으로도 False로 남아있는지를 판단하는 것으로 원소의 종류가 완벽히 동일한지를 알아낼 수 있게 됩니다. 이때 걸리는 시간은 $O(N1 + N2)$ 가 됩니다.

```python
arr1 = [1, 2, 5, 3, 2]
set1 = set(arr1)

arr2 = [5, 5, 2, 3, 1, 2, 2, 5]
set2 = set(arr2)

not_exist = False

for elem1 in arr1:
    if elem1 not in set2:
        not_exist = True

for elem2 in arr2:
    if elem2 not in set1:
        not_exist = True

if not_exist == False:
    print("Same!")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.