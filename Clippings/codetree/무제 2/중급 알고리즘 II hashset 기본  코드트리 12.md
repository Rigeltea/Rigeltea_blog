---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-process-numeric-commands-6/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 5. Priority Queue

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 우선순위 큐

앞서 큐(Queue)는 먼저 들어오는 데이터가 먼저 나가는 선입선출(FIFO) 형식의 자료구조라고 배웠습니다.

우선순위 큐(Priority Queue)는 이와 다르게 항상 우선순위가 가장 높은 데이터에만 관심이 있고, 이 데이터만 먼저 나갈 수 있는 형태의 자료구조입니다. 이는 배열, 연결 리스트를 통해서도 구현이 가능하지만, 힙을 이용해야지만이 삽입, 삭제 시간을 $O(logN)$ 으로 맞출 수가 있기 때문에 보통 힙을 이용하여 우선순위큐를 구현하고는 합니다.

python에 PriorityQueue라는 class가 있기는 하지만 이는 알고리즘 문제를 풀기 위해 나온 class가 아니라 thread간의 synchronized를 맞춰야 하는 제약이 있는 class이기 때문에 사용시 속도가 굉장히 느려집니다. **따라서 python에서 제공하는 heapq를 사용해 PriorityQueue를 대신하여 이용하고는 합니다.** heapq 사용을 위해서는 `import heapq` 를 가장 위에 적어줘야 합니다. 단, 이 heapq는 기본적으로 min-heap인데, 보통 우선순위 큐를 이용하는 경우에는 **최댓값을 찾는** 경우가 더 자주 발생하기 때문에, 연습을 위해 PriorityQueue이라는 class를 직접 만들어 heapq를 이용해 클래스 내 함수를 정의한 뒤, 정의된 PriorityQueue 클래스를 이용해 보겠습니다. 다만 heapq는 min-heap이므로 이를 max-heap처럼 사용하기 위해서는 넣는 값에 `-` 를 붙여 관리하여 마치 최댓값이 골라지는 것과 같은 효과를 만들어내야 합니다. 이 부분은 완벽하게 이해하지 않으셔도 괜찮습니다.

```python
class PriorityQueue:
    def __init__(self):          # 빈 Priority Queue 하나를 생성합니다.
        self.items = []
                
    def push(self, item):        # 우선순위 큐에 데이터를 추가합니다.
        heapq.heappush(self.items, -item)
                
    def empty(self):             # 우선순위 큐가 비어있으면 True를 반환합니다.
        return not self.items
                
    def size(self):              # 우선순위 큐에 있는 데이터 수를 반환합니다.
        return len(self.items)
        
    def pop(self):               # 우선순위 큐에 있는 데이터 중 최댓값에 해당하는 데이터를 반환하고 제거합니다.
        if self.empty():
            raise Exception("PriorityQueue is empty")
            
        return -heapq.heappop(self.items)
                
    def top(self):               # 우선순위 큐에 있는 데이터 중 최댓값에 해당하는 데이터를 제거하지 않고 반환합니다.
        if self.empty():
            raise Exception("PriorityQueue is empty")
                        
        return -self.items[0]
```

PriorityQueue를 이용할 때 자주 사용되는 것은 다음 5가지 입니다.

1. `push(E)`

우선순위 큐에 데이터 E를 추가합니다.

2. `size()`

현재 우선순위 큐에 들어있는 데이터의 수를 반환합니다.

3. `empty()`

현재 우선순위 큐가 비어있다면 true, 아니라면 false를 반환합니다.

4. `top()`

우선순위 큐에서 최댓값에 해당하는 데이터를 반환합니다.

5. `pop()`

우선순위 큐에서 최댓값에 해당하는 데이터를 반환합니다. 동시에 그 데이터를 우선순위 큐에서 뺍니다.

따라서 다음과 같이 코드를 작성해볼 수 있습니다.

```python
import heapq

class PriorityQueue:
    def __init__(self):          # 빈 Priority Queue 하나를 생성합니다.
        self.items = []
                
    def push(self, item):        # 우선순위 큐에 데이터를 추가합니다.
        heapq.heappush(self.items, -item)
                
    def empty(self):             # 우선순위 큐가 비어있으면 True를 반환합니다.
        return not self.items
                
    def size(self):              # 우선순위 큐에 있는 데이터 수를 반환합니다.
        return len(self.items)
        
    def pop(self):               # 우선순위 큐에 있는 데이터 중 최댓값에 해당하는 데이터를 반환하고 제거합니다.
        if self.empty():
            raise Exception("PriorityQueue is empty")
            
        return -heapq.heappop(self.items)
                
    def top(self):               # 우선순위 큐에 있는 데이터 중 최댓값에 해당하는 데이터를 제거하지 않고 반환합니다.
        if self.empty():
            raise Exception("PriorityQueue is empty")
                        
        return -self.items[0]

pq = PriorityQueue()          # 우선순위 큐를 선언합니다. => 빈 우선순위 큐
pq.push(2) 
pq.push(9)
pq.push(5)
    
print(pq.top())       # 최댓값을 출력합니다. => 9
pq.pop()              # 최댓값을 제거합니다.
print(pq.size())      # 원소의 개수를 출력합니다 => 2
while not pq.empty(): # 최댓값을 갖는 원소부터 순서대로 출력합니다.
  print(pq.top())     # 순서대로 5 2가 출력됩니다.
  pq.pop()            # 최댓값에 해당하는 원소를 뺍니다.
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.