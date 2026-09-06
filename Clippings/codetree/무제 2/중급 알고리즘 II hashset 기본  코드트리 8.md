---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-find-maximum-number/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. TreeSet

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 원하는 값을 삭제하며 최댓값 유지하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, -6, 7, -7, -2] 와 같이 숫자들이 순서대로 주어졌을 때,
각각의 숫자가 주어질 때 마다 지금까지 주어진 숫자들 중 
최댓값을 출력하는 프로그램을 작성해보세요.

단, 음수가 주어지면 해당 숫자에 -1을 곱한 양수 값을 찾아 제거해줍니다. 
이 숫자를 제외한 숫자들 중 최댓값을 출력해야 합니다.
```

무작정 코드를 작성한다면, 숫자가 주어질 때마다 앞에 있는 숫자들을 전부 탐색해 그 중에서도 아직 삭제되지 않은 숫자들 중 최댓값을 골라야 합니다. 이 방법의 시간복잡도는 $O(N^2)$ 이 됩니다.

이를 개선시킬 수 있습니다.  
지금까지 살펴본 숫자들 중 최댓값을 계속 구해주며, 그 중 원하는 숫자를 지속적으로 제거해주는 과정을 빠르게 할 수 있도록 도와주는 자료구조는 바로 treeset 입니다. 최댓값만 계속 구해주는 것은 Priority Queue (우선순위 큐)를 이용해도 가능하지만, 우선순위 큐의 경우에는 삭제 연산을 최댓값에 대해서만 진행할 수 있기 때문에 원하는 원소를 직접 골라 자유자재로 삭제하는 것은 불가능합니다. 따라서 이 경우에는 treeset을 이용해볼 수 있으며 최댓값을 찾는 과정이 $O(logN)$, 원하는 값을 삭제하는 과정 역시 $O(logN)$ 에 가능합니다. 따라서 총 시간복잡도가 $O(NlogN)$ 이 됩니다.

코드는 다음과 같이 작성해볼 수 있습니다.

```python
from sortedcontainers import SortedSet

arr = [3, 6, 2, -6, 7, -7, -2]
s = SortedSet()

for elem in arr:
    if elem > 0:          # 양수인 경우에는
        s.add(elem)       # treeset에 넣어줍니다.
    else:                 # 음수인 경우에는
        s.remove(-elem)   # treeset에서 제거해줍니다.
    
    print(s[-1], end=" ") # 최댓값을 출력해줍니다.

>> 출력 : 3 6 6 3 7 3 3
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.