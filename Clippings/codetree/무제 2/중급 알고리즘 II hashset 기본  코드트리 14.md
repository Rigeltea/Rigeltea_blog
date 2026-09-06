---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-min-integer-output/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. Priority Queue

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 현재까지의 최솟값을 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, 6, 7, 7, 2] 와 같이 숫자들이 순서대로 주어졌을 때,
각각의 숫자가 주어질 때 마다 지금까지 주어진 숫자들 중 
최솟값을 출력하는 프로그램을 작성해보세요.
```

무작정 코드를 작성한다면, 숫자가 주어질 때마다 앞에 있는 숫자들을 전부 탐색해 그 중 최솟값을 골라야 합니다. 이 방법의 시간복잡도는 $O(N^2)$ 이 됩니다.

이를 priority\_queue를 이용하여 각 최솟값을 찾는 과정을 $O(logN)$ 에 해결해 총 시간복잡도 $O(NlogN)$ 으로 해결할 수 있습니다.

코드는 다음과 같습니다.

```python
import heapq

arr = [3, 6, 2, 6, 7, 7, 2]
pq = []

for elem in arr:
    heapq.heappush(pq, elem) # priority queue에 넣어줍니다.

    print(pq[0], end=" ")    # 최솟값을 출력합니다.

>> 출력 : 3 3 2 2 2 2 2
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.