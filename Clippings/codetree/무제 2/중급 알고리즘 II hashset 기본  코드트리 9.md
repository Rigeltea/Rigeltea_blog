---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-nearest-number/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. TreeSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 인접한 두 숫자를 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[1, 5, 2, 10, 6] 와 같이 숫자들이 주어져 있는 상황에서
숫자 9와 가장 가까이에 있는 
양쪽 두 숫자를 구하는 프로그램을 작성해보세요.
```

숫자 9의 바로 오른쪽에 있는 숫자의 위치는 bisect\_right 함수를 이용하면 바로 구할 수 있습니다. 그렇다면 바로 왼쪽에 있는 숫자의 위치는 어떻게 구해볼 수 있을까요?

bisect\_right 함수는 index를 반환해주므로, 이 index 값에 1을 빼주면 바로 왼쪽 숫자의 위치가 나오게 될 것입니다. 따라서 이 문제에서는 bisect\_right 함수를 이용해 x보다 큰 최초의 위치를 구한 후, 위치를 1만큼 감소시키면 x보다 작은 최초의 위치를 바로 알아낼 수 있게 됩니다.

```python
from sortedcontainers import SortedSet

s = SortedSet()

s.add(1)
s.add(5)
s.add(2)
s.add(10)
s.add(6)

x = 9

r_idx = s.bisect_right(x)  # x보다 큰 최초의 위치를 찾습니다.
print(s[r_idx])            # 해당 값을 출력합니다. (10)

l_idx = r_idx - 1          # 바로 직전의 위치를 구합니다.
print(s[l_idx])            # 해당 값을 출력합니다. (6)

>> 10
    6
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.