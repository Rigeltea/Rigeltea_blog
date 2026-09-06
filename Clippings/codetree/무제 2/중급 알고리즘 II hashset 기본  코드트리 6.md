---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-find-number-fast-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. TreeSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 같거나 큰 숫자 중 최솟값 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, -6, 7, -7, -2, -8] 와 같이 숫자들이 순서대로 주어졌을 때,
음수가 주어질 때마다 해당 음수를 x라 했을 때,  
현재까지 주어진 숫자들 중 -x보다 같거나 큰 최소 숫자를 출력하는
프로그램을 작성해보세요. 만약 없다면 -1을 출력합니다.
```

무작정 코드를 작성한다면, 숫자가 주어질 때마다 앞에 있는 숫자들을 전부 탐색해 그 중에서 -x보다 같거나 큰 숫자들 중 최솟값을 골라야 합니다. 이 방법의 시간복잡도는 $O(N^2)$ 이 됩니다.

이를 개선시킬 수 있습니다.  
지금까지 살펴본 숫자들 중 특정 숫자 k보다 같거나 큰 숫자를 빠르게 구할 수 있도록 도와주는 자료구조는 바로 treeset 입니다. treeset을 이용하면 특정 값보다 같거나 큰 숫자를 구하는 과정이 $O(logN)$ 에 가능합니다. 따라서 총 시간복잡도가 $O(NlogN)$ 이 됩니다.

코드는 다음과 같이 작성해볼 수 있습니다.

```python
from sortedcontainers import SortedSet

arr = [3, 6, 2, -6, 7, -7, -2, -8]
s = SortedSet()

for elem in arr:
    if elem > 0:                 # 양수인 경우에는
        s.add(elem)              # treeset에 넣어줍니다.
    else:                        # 음수인 경우에는 같거나 큰 최초의 위치를 확인합니다.
        if s.bisect_left(-elem) == len(s):   # 같거나 큰 위치가 없다면
            print(-1, end=" ")               # -1을 출력합니다.
        else:
            print(s[s.bisect_left(-elem)], end=" ") # 있다면 해당 값을 출력합니다.

>> 출력 : 6 7 2 -1
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.