---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-nearest-point/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. Priority Queue

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 원하는 기준에 맞춰 정렬하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[(1, 7), (3, 2), (3, 1), (6, 2)] 와 같이 2차 평면상의 
점들의 위치가 순서대로 주어졌을 때,
각각의 점의 위치가 주어질 때 마다 지금까지 주어진 점들 중 
x, y의 곱이 가장 큰 경우를 출력하는 프로그램을 작성해보세요.
```

무작정 코드를 작성한다면, 점의 위치가 주어질 때마다 앞에 있는 점들을 전부 탐색해 그 중 곱이 최대가 되는 경우를 골라야 합니다. 이 방법의 시간복잡도는 $O(N^2)$ 이 됩니다.

이때 역시 priority\_queue를 이용할 수 있습니다. priority\_queue를 이용하면 각 최댓값을 찾는 과정이 $O(logN)$ 이 되므로 총 시간복잡도 $O(NlogN)$ 이 됩니다.

주어진 문제에서 처럼 하나의 숫자가 아닌 여러 값들로부터 하나의 객체가 만들어지는 경우에 python에서는 tuple type을 사용합니다. 이러한 [객체](https://www.codetree.ai/missions/5/concepts/41/problems/007/introduction) 에 대해 잘 모르신다면, 객체에 대해 공부를 진행한 후 이 글을 읽는 것을 추천드립니다.

만약 x좌표 순으로 가장 큰 점을 찾고, x좌표가 큰 점이 여러 개라면 그 중 y값이 가장 큰 점을 찾는 문제였다면 다음과 같이 `tuple` type으로 priority\_queue를 이용하면 알아서 첫 번째 값을 첫 번째 우선순위로 하고, 두 번째 값을 두 번째 우선순위로 하여 최댓값을 골라주게 됩니다. 단, python에서의 heapq는 기본적으로 최솟값을 구해주기 때문에, **더 큰 값이 먼저 나오도록 하기 위해서는 해당 위치에 꼭 -를 붙여서 이용해야 함에 유의합니다.**

```python
import heapq

points = [
    (1, 7), (3, 2), (3, 1), (6, 2)
]
pq = []

for point in points:
    x, y = point
    heapq.heappush(pq, (-x, -y)) # priority queue에 넣어줍니다.
                          # 단, x, y 모두 큰 값이 먼저 나오기를 원하므로
                          # -를 붙여서 넣어줍니다.

    best_point = pq[0]    # x, y 순으로 가장 우선순위가 높은 경우를 찾아줍니다.
    best_x, best_y = best_point

    print(-best_x, -best_y) # -를 붙여서 이용했으므로 사용할 때에는 다시 -를 꼭 붙여줘야 합니다.

>> 출력 : 1 7
2
2
2
```

하지만 이 문제에서는 곱이 최대가 되는 경우를 원하기 때문에, 이 곱이 우리가 원하는 우선순위에 들어가야 합니다. 이를 가장 손쉽게 해결할 수 있는 방법은 **곱에 해당하는 값을 직접 만들어 객체의 첫 번째 값으로 설정하는 것입니다.** 즉, `tuple` 에 3가지 값을 넣는 식으로 진행합니다. 첫 번째 값으로는 x, y의 곱, 두 번째 값으로는 x, 세 번째 값으로는 y를 넣어 첫 번째 우선순위인 두 값의 곱으로 자동으로 최댓값이 뽑히도록 만들어 줄 수 있습니다. 단, 이 경우에도 큰 값이 먼저 나오도록 해야하므로 첫 번째 값에는 꼭 -를 붙여서 진행해야 함에 유의합니다. x, y값 자체는 우선순위와 관계가 없으므로 굳이 -를 붙이지 않고 진행해도 됩니다.

```python
import heapq

points = [
    (1, 7), (3, 2), (3, 1), (6, 2)
]
pq = []

for point in points:
    x, y = point
    heapq.heappush(pq, (-(x * y), x, y)) # priority queue에 넣어줍니다.
                          # 단, x * y값이 큰 것이 먼저 나오기를 원하므로
                          # -를 붙여서 넣어줍니다.

    best_point = pq[0]    # x * y 순으로 가장 우선순위가 높은 경우를 찾아줍니다.
    _, best_x, best_y = best_point # 우리가 원하는 x, y 값만 tuple에서 가져와줍니다.

    print(best_x, best_y)

>> 출력 : 1 7
7
7
2
```

이렇듯 원하는 우선순위에 따라 해당하는 값을 직접 추가해주는 식으로 원하는 결과를 얻어낼 수 있습니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.