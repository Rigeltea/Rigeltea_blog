---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-keep-picking-the-big-number/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. Priority Queue

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 현재까지의 최댓값을 빠르게 구하기

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
[3, 6, 2, 6, 7, 7, 2] 와 같이 숫자들이 순서대로 주어졌을 때,
각각의 숫자가 주어질 때 마다 지금까지 주어진 숫자들 중 
최댓값을 출력하는 프로그램을 작성해보세요.
```

무작정 코드를 작성한다면, 숫자가 주어질 때마다 앞에 있는 숫자들을 전부 탐색해 그 중 최댓값을 골라야 합니다. 이 방법의 시간복잡도는 $O(N^2)$ 이 됩니다.

이를 개선시킬 수 있습니다.  
지금까지 살펴본 숫자들 중 최댓값을 계속 구해주는 것은 treeset으로도 가능했지만, priority queue를 사용하는 것 역시 가능합니다. 여기서는 priority queue를 사용해 보도록 하겠습니다. priority queue를 이용하면 최댓값을 찾는 과정을 $O(logN)$ 에 할 수 있습니다. 따라서 총 시간복잡도가 $O(NlogN)$ 이 됩니다.

이번에는 heapq를 직접 사용하여 priority queue를 이용해보려고 합니다. heapq는 다음 5개의 문법을 잘 알고 계시면 됩니다.

1. 원소 추가

`heapq.heappush()` 함수를 이용하면 됩니다.  
첫 번째 인자에는 priority queue에 해당하는 리스트를 넘겨줘야 하며, 두 번째 인자에 추가할 원소를 넣어주시면 됩니다. heapq는 기본적으로 min-heap이 때문에 최솟값을 구해줌에 유의합니다. 이때 최솟값은 0번지 인덱스에 들어있습니다.

```python
import heapq

pq = []
heapq.heappush(pq, 3) 
heapq.heappush(pq, 5)

print(pq[0])   # 최솟값 3
```

2. 최솟값 제거

`heapq.heappop()` 함수를 이용하면 됩니다.  
최솟값을 제거하고자 하는 priority queue에 해당하는 리스트를 첫 번째 인자로 넘겨주시면 됩니다.

```python
import heapq

pq = []
heapq.heappush(pq, 3) 
heapq.heappush(pq, 5)

print(pq[0])        # 최솟값 3
heapq.heappop(pq)   # 최솟값을 제거
print(pq[0])        # 최솟값 5
```

3. 원소의 수 조회

내장함수인 `len()` 을 이용하면 됩니다.

```python
import heapq

pq = []
heapq.heappush(pq, 3) 
heapq.heappush(pq, 5)

print(len(pq))      # 원소의 개수 = 2개
heapq.heappop(pq)   # 최솟값을 제거
print(len(pq))      # 원소의 개수 = 1개
```

4. heapq가 비어있는지 조회

`if pq:` 형태로 활용하시면 됩니다.

```python
import heapq

pq = []
heapq.heappush(pq, 3)

if pq:             # 원소가 남아있다면
    print(pq[0])   # 최솟값을 출력
```

5. 최솟값 찾기

0번지 값을 이용하시면 됩니다.

```python
import heapq

pq = []
heapq.heappush(pq, 3) 
heapq.heappush(pq, 5)

print(pq[0])   # 최솟값 3
```

만약 priority queue를 max-heap으로서 최댓값을 관리하도록 하고 싶다면, 숫자에 -를 붙여 진행하는 트릭을 사용해볼 수 있습니다. -가 붙게 되면 실제 최댓값에 해당하는 숫자가 가장 우선순위가 높아 지기 때문에, **값을 넣기 전에 -를 붙이고, 값을 사용하기 전에 다음과 같이 -를 다시 붙여 사용하는 식** 으로 간단히 최댓값을 구해줄 수 있습니다.

코드는 다음과 같이 작성해볼 수 있습니다.

```python
import heapq

arr = [3, 6, 2, 6, 7, 7, 2]
pq = []

for elem in arr:
    heapq.heappush(pq, -elem) # priority queue에 넣어줍니다.

    print(-pq[0], end=" ")    # 최댓값을 출력합니다.

>> 출력 : 3 6 6 6 7 7 7
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.