---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-count-number-of-points-3/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Grid Compression

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 좌표 압축

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
다음과 같이 정점 번호가 1에서 10^9 사이의 값으로 이루어져 있는
그래프가 하나 주어졌을 때,

1번 정점에서 시작하여 방문 가능한 서로 다른 노드의 수를 구하는 프로그램을 작성해보세요.
```

![Image](https://contents.codetree.ai/problem_factory/images/7cfbbbc8-4cec-461c-a86a-349ce2d519f0.webp)

일반적인 DFS 탐색은 1번 정점에서 N번 정점까지 번호가 매겨져 있기 때문에, 큰 문제 없이 크기가 N인 visited 배열과 간선 정보를 나타내는 인접리스트를 만들어 해결할 수 있습니다. 하지만 위와 같이 정점 번호가 1에서 $10^9$ 사이로 주어진 경우에는 기존 방법으로 해결하기가 어렵습니다.

이때 사용할 수 있는 방법이 바로 좌표 압축(Grid Compression) 입니다.

주어진 정점 번호를 오름차순으로 나열하면 $1, 4, 6, 7, 30, 2000, 10^9$ 이 됩니다. 이 정점들의 번호를 1번부터 순서대로 다시 매겨주는 것입니다. 즉, 다음과 같이 번호를 변경해주는 작업을 진행해보는 것입니다.

```
1     -> 1
4     -> 2
6     -> 3
7     -> 4
30    -> 5
2,000 -> 6
10^9  -> 7
```

이렇게 변경을 하게 되면, 마치 1~N 사이의 번호로 정점이 주어졌던 기존 문제처럼 문제를 해결할 수 있게 됩니다.

![](https://contents.codetree.ai/problems/2273/images/introductions-8c7b5a7a-918a-4731-bbde-a4dd0067ffd1.png)

이 과정은 다음의 두 과정을 거쳐서 진행해볼 수 있습니다.

1. 먼저 입력으로 들어온 모든 값을 treeset에 넣어줍니다.
2. 작은 숫자부터 순서대로 뽑아, 각 숫자에 번호를 매기고 그 결과를 hashmap에 넣어줍니다. 위의 예에서는 (1, 1), (4, 2), (6, 3), (7, 4), (30, 5), (2000, 5), (10^9, 7) 형태로 hashmap에 들어가게 됩니다.

이 과정을 진행하고 나면, hashmap을 이용해 주어진 정점 번호를 1에서 N번 사이로 변경해줄 수 있게 됩니다.

코드는 다음과 같습니다.

```python
from sortedcontainers import SortedSet

edges = [
    (1, 10**9), (1, 2000), (1, 4), (30, 10**9), (6, 7)
]

nums = SortedSet()

# 사용되는 모든 번호를 treeset에 넣어줍니다.
for v1, v2 in edges:
    nums.add(v1)
    nums.add(v2)

# treeset에서 정점을 작은 번호부터 뽑으면서
# 각 정점별로 1번부터 순서대로 매칭하여
# 그 결과를 hashmap에 넣어줍니다.
mapper = dict()
cnt = 1
for num in nums:
    mapper[num] = cnt
    # 기존 정점번호마다 어떤 번호로
    # 정해졌는지를 출력해봅니다.
    print(num, "->", cnt)
    cnt += 1

# 주어진 간선을 이루는 정점 번호를
# 새로운 정점 번호로 변경해줍니다.
for i in range(5):
    v1, v2 = edges[i]
    edges[i] = (mapper[v1], mapper[v2])

>> 출력:
1 -> 1
4 -> 2
6 -> 3
7 -> 4
30 -> 5
2000 -> 6
1000000000 -> 7
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.