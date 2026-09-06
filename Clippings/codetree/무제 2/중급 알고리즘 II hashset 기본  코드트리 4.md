---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-treeset-basic/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. TreeSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## SortedSet

Python에서는 TreeSet 자료구조로 만들어져있는 built-in function (내장함수)이 없습니다. 따라서 여기서는 [sortedcontainers](http://www.grantjenks.com/docs/sortedcontainers/) 라는 외부 라이브러리를 사용하도록 하겠습니다.

여기 sortedconainters에서 SortedSet라는 Class를 이용할 수 있습니다. SortedSet은 TreeSet 자료구조로 되어있으며, 이 TreeSet이 바로 [균형잡힌이진트리](https://www.codetree.ai/missions/6/concepts/33/problems/balanced-binary-tree/introduction) 구조로 데이터들을 관리해주는 자료구조 입니다. 따라서 삽입, 삭제, 탐색 등 모든 함수의 시간복잡도가 전부 $O(logN)$ 입니다.

SortedSet은 `from sortedcontainers import SortedSet` 를 적어줘야 사용이 가능합니다.

```python
from sortedcontainers import SortedSet

s = SortedSet()      # treeset
```

SortedSet을 이용할 때 자주 사용되는 것은 다음 7가지 입니다.

1. `s.add(E)`

treeset에 데이터 E를 추가합니다.

2. `s.remove(E)`

현재 treeset에 들어있는 데이터 중 E를 찾아 제거합니다.

3. `E in s`

현재 treeset에 숫자 E가 들어 있는지를 확인합니다. 있다면 True, 없다면 False를 반환합니다.

4. `s.bisect_left(E)`

SortedSet 내에 있는 값들을 오름차순으로 정렬했다고 가정했을 때, E보다 같거나 큰 최초의 데이터가 들어있는 index 값을 반환합니다. 만약 없다면 SortedSet내에 있는 데이터의 수에 해당하는 값을 반환합니다. 따라서 같거나 큰 최초의 데이터 값을 얻기 위해서는 bisect\_left로 나온 index에 해당하는 값을 s에서 꺼내줘야 합니다.

```python
from sortedcontainers import SortedSet

s = SortedSet([10, 15])
print(s.bisect_left(9))  # 9보다 같거나 큰 최초 숫자의 위치 = 0
print(s.bisect_left(10)) # 10보다 같거나 큰 최초 숫자의 위치 = 0
print(s.bisect_left(11)) # 11보다 같거나 큰 최초 숫자의 위치 = 1
print(s.bisect_left(16)) # 16보다 같거나 큰 최초 숫자의 위치 = 2

idx = s.bisect_left(9)   # 9보다 같거나 큰 최초 숫자의 위치 = 0
print(s[idx])            # 9보다 같거나 큰 최초 숫자 값 = 10
```

5. `s.bisect_right(E)`

SortedSet 내에 있는 값들을 오름차순으로 정렬했다고 가정했을 때, E보다 큰 최초의 데이터가 들어있는 index 값을 반환합니다. 만약 없다면 SortedSet내에 있는 데이터의 수에 해당하는 값을 반환합니다. 따라서 같거나 큰 최초의 데이터 값을 얻기 위해서는 bisect\_right로 나온 index에 해당하는 값을 s에서 꺼내줘야 합니다.

```python
from sortedcontainers import SortedSet

s = SortedSet([10, 15])
print(s.bisect_right(9))  # 9보다 큰 최초 숫자의 위치 = 0
print(s.bisect_right(10)) # 10보다 큰 최초 숫자의 위치 = 1
print(s.bisect_right(11)) # 11보다 큰 최초 숫자의 위치 = 1
print(s.bisect_right(16)) # 16보다 큰 최초 숫자의 위치 = 2

idx = s.bisect_right(10)  # 10보다 큰 최초 숫자의 위치 = 1
print(s[idx])             # 10보다 큰 최초 숫자 값 = 15
```

6. `s[0]`

기본적으로 treeset은 오름차순 정렬을 해줍니다. 따라서 treeset의 첫 번째 값인 `s[0]` 에 들어있는 값은 treeset에 적혀있는 값들 중 가장 작은 값이 됩니다. 즉, 가장 작은 값은 `s[0]` 으로 조회가 가능합니다.

7. `s[-1]`

기본적으로 treeset은 오름차순 정렬을 해준다고 했습니다. 따라서 treeset에서 가장 큰 값은 가장 마지막 위치에 들어 있을 것입니다. 즉, 가장 큰 값은 `s[-1]` 로 조회가 가능합니다.

코드는 다음과 같이 작성해볼 수 있습니다.

```python
from sortedcontainers import SortedSet

s = SortedSet()             # treeset을 선언합니다.
s.add(3)
s.add(9)
s.add(5)

if 3 in s:                  # 숫자 3이 treeset에 있다면
    print("exists!")

print(s[s.bisect_left(3)])  # 숫자 3보다 같거나 큰 최초의 숫자를 출력합니다 => 3
print(s[s.bisect_right(3)]) # 숫자 3보다 큰 최초의 숫자를 출력합니다 => 5

print(s[0])                 # 가장 작은 원소를 출력합니다 => 3
print(s[-1])                # 가장 큰 원소를 출력합니다 => 9

s.remove(9)                 # 숫자 9를 제거합니다.
if 9 not in s:              # 숫자 9가 treeset에 없다면
    print("not exists!")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.