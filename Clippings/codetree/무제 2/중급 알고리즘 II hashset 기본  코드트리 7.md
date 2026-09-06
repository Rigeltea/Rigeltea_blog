---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-frendly-point/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. TreeSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 기준이 여러 개일 때의 lower, upper bound

다음 문제는 어떻게 해결해 볼 수 있을까요?

```python
사람들의 키와 몸무게 정보가 주어졌을 때,
주어진 (height, weight)를 기준으로
우선순위가 가장 높은 사람을 찾는 프로그램을 작성해보세요.

1. 키가 height와 동일하면서 몸무게가 weight보다 같거나 큰 사람이 있다면 
   그 중 몸무게가 가장 적은 사람을 선택합니다.
2. 1을 만족하는 사람이 없다면,
   키가 height보다 큰 사람들 중 키가 가장 작은 사람을 찾습니다. 
   만약 키가 작은 사람이 여러 명이라면, 그 중 몸무게가 가장 작은 사람을 골라주세요.

예를 들어
[(170, 60), (160, 55), (180, 82), (185, 77), (170, 30)] 이렇게 사람 정보가 주어졌을 때

(height, weight)값이 (165, 50) 이었다면, 키 165 이상이면서 가장 키가 작은 경우는 
,
(170, 30)이 답이 됩니다.
```

무작정 코드를 작성한다면, 모든 사람에 대해 조사해봐야 하므로 $O(N)$ 의 시간이 소요됩니다.  
만약 이렇듯 특정 (height, weight) 기준으로 같거나 큰 최초의 사람을 찾아야 하는 경우가 Q번 있다면 총 시간복잡도는 $O(QN)$ 이 될 것입니다.

이렇게 기준이 여러 개인 경우에도 SortedSet의 bisect\_left, bisect\_right를 이용할 수 있습니다.

예로 Python에서는 tuple이라는 type을 이용하면 2개 이상의 값을 하나의 데이터로 하여 저장할 수 있습니다. 여기서는 (height, weight) 쌍이 하나의 데이터이므로, `p = tuple(height, weight)` 이런 식으로 데이터를 만들어 줄 수 있습니다. 표현해야 하는 데이터 수가 3개 이상인 경우에도 tuple을 이용하면 되며, class를 직접 만들어 이용하는 것 역시 가능합니다. 각 데이터를 표현하기 위해 class, tuple을 이용하는 방법에 대해 아직 잘 모르신다면, Novice Mid 문제집의 [객체](https://www.codetree.ai/missions/5/concepts/41/problems/007/introduction) 유형을 공부하신 이후에 이 글을 읽는 것을 추천드립니다.

```python
from sortedcontainers import SortedSet

s = SortedSet()

s.add((170, 60))
s.add((160, 55))
s.add((180, 82))
s.add((185, 77))
s.add((170, 30))
```

이렇게 만들어진 SortedSet에 bisect\_left를 적용하면 tuple의 1번째에 적힌 값(여기서의 height)을 기준으로 같거나 크면서 값이 가장 작은 것을 찾아주고, 만약 그러한 값이 여러 개라면 그 중 2번째 값을 기준으로 값이 가장 작은 경우를 찾아줍니다. 따라서 (165, 50)을 기준으로 bisect\_left 적용시 (170, 30) 사람의 위치가 찾아지게 됩니다.

```python
from sortedcontainers import SortedSet

s = SortedSet()

s.add((170, 60))
s.add((160, 55))
s.add((180, 82))
s.add((185, 77))
s.add((170, 30))

best_person = s[s.bisect_left((165, 50))]
height, weight = best_person
print(height, weight)

>> 출력 결과 : 170 30
```

SortedSet의 bisect\_left 함수의 시간복잡도는 $O(logN)$ 이므로, 이러한 질문이 Q개가 들어온다 했을 때의 총 시간복잡도는 $O(QlogN)$ 이 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.