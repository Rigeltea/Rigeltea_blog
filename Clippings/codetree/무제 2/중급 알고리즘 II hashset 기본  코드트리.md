---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-hashset-basic/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. HashSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## set

Python에서는 set이라는 class가 있습니다. set은 HashSet 자료구조로 되어있으며, 이 HashSet이 바로 [해싱](https://www.codetree.ai/missions/6/problems/hash-introduction/introduction) 을 기반으로 데이터들을 관리해주는 자료구조 입니다. 따라서 삽입, 삭제, 탐색 등 모든 함수의 시간복잡도가 전부 $O(1)$ 입니다. HashSet은 빠르지만, 구조 특성상 들어온 값들간의 순서를 나타내주지 못합니다.

set을 사용하기 위해서는 `set()` 형태로 선언하면 됩니다. 만약 리스트를 set으로 변경하고 싶다면 `set([1, 3, 5])` 처럼 넣어줄 수 있으며, 처음부터 `{1, 3, 5}` 같은 집합 형태로 set을 정의할 수도 있습니다. 또, python에서의 set은 type에 제한이 없습니다. 예시는 다음과 같습니다.

```python
s1 = set()                             # {}
s2 = {1, 3, 5}                         # {1, 3, 5}
s3 = set([1, 3, 5])                    # {1, 3, 5}
s4 = set([1, 3, (2, 5), "hello"])      # {1, 3, (2, 5), "hello"}
s5 = {3, 5, [1, 5]}                    # error - list는 unhashable type
```

다만 s5의 경우 **리스트** 를 하나의 원소로 set에 넣으려고 하다보니 에러가 발생하게 됩니다. set의 원소가 될 수 있는 값들은 **전부 immutable 한 값들 뿐입니다.** python에서 immutable한 type은 int, char 등의 primitive type과 string, tuple 등인데 mutable한 list, dict 등의 type은 가변적이기 때문에 set의 원소로서 적용할 수 없는 것입니다.

set을 이용할 때 자주 사용되는 것은 다음 3가지 입니다. `s = set()` 을 가정하고 살펴보겠습니다.

1. `s.add(E)`

hashset에 데이터 E를 추가합니다.

2. `s.remove(E)`

현재 hashset에 들어있는 데이터 중 숫자 E를 찾아 제거합니다.

3. `E in s`

현재 hashset에 숫자 E가 들어 있는지를 찾습니다. 있다면 True, 아니라면 False를 반환합니다. 마찬가지 이유로 `E not in s` 라는 구문 역시 사용 가능합니다.

코드는 다음과 같이 작성해볼 수 있습니다.

```python
s = set()                # 정수를 관리할 hashset을 선언합니다. => 빈 set
s.add(3)
s.add(9)
s.add(5)
    
if 3 in s:               # 숫자 3이 set에 있다면
    print("exists!")

s.remove(9)              # 숫자 9를 제거합니다.
if 9 not in s:           # 숫자 9가 hashset에 없다면
    print("not exists!")
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.