---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-traveling-salesman-problem-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. Bitmask DP

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Bitmask DP

다음 문제는 어떻게 해결해볼 수 있을까요?

```
아래와 같이 노드가 4개 간선이 x개 있는 양방향 그래프가 주어져있습니다. 
3번 노드에서 시작하여 모든 노드를 정확히 한번씩만 방문하되,
이동거리의 합이 최소가 되도록 해보세요.
```

![](https://contents.codetree.ai/problems/3454/images/introductions-7ea3bc4f-6e63-408f-b28b-1bd672de8084.png)

3번에서 시작하여 모든 정점을 단 한번씩만 방문해야 하는 문제이므로 가장 간단한 방법은 모든 순열을 만들어보는 백트래킹을 이용하는 것입니다. 백트래킹을 이용해 모든 순열을 만드는 방법에 대해 아직 잘 모르신다면, [순열 만들기](https://www.codetree.ai/missions/2/problems/n-permutation/introduction) 유형을 공부하시고 나서 다시 이 설명을 읽는 것을 추천드립니다.

백트래킹을 이용한 코드는 아래와 같습니다. 가능한 모든 순열을 만들어야 하므로 시간복잡도는 $O(N!)$ 이 됩니다.

```python
import sys

INT_MAX = sys.maxsize

n = 4
dist = [
    [0, 1, 3, 4],
    [1, 0, 9, 5],
    [3, 9, 0, 6],
    [4, 5, 6, 0]
]
visited = [False] * n

ans = INT_MAX

# 지금까지 cnt개의 정점을 방문했고
# 현재 위치 x에 있고
# 지금까지의 이동거리의 합이 sum_dist라 했을 때 
# 모든 정점을 방문하기 위한 시뮬레이션을 진행하여
# 그 중 최적의 값을 구합니다.
def find_max(cnt, x, sum_dist):
    global ans

    # 종료조건입니다.
    if cnt == n:
        ans = min(ans, sum_dist)
        return

    for i in range(n):
        if visited[i]:
            continue
        
        visited[i] = True
        find_max(cnt + 1, i, sum_dist + dist[x][i])
        visited[i] = False

# 3번 지점에서 시작하여
# 최적의 답을 구합니다.
visited[3] = True
find_max(1, 3, 0)
print(ans)
```

이 문제는 bimask DP를 이용하여 $O(2^N \times N^2)$ 에도 해결해볼 수 있습니다.

3번 정점에서 시작하여 **(1) 지금까지 방문한 노드의 종류가 아예 동일하고, (2) 동시에 현재 서있는 노드의 위치가 동일하고, (3) 지금까지의 이동거리가 동일한 경우** 즉, 예로 아래와 같이 두 상황은 아예 동등한 상황이라고 생각해볼 수 있습니다.

![](https://contents.codetree.ai/problem_factory/images/6758f061-f69f-4bd0-a2e6-7434c26c7755.webp)

따라서 이 문제는 **(1) 지금까지 방문한 노드의 종류가 동일하고, (2) 현재 서있는 노드의 위치가 동일한 상태** 에서 이동거리를 최소화하는 DP로 해결이 가능합니다.

`dp[i][j]를 3번을 시작으로 겹치지 않게 방문한 위치에 해당하는 상태가 i이고 그래서 현재 서 있는 위치가 j가 되었을 때 가능한 최소 이동 거리` 가 됩니다. 이때 방문한 위치들에 해당하는 상태를 나타내는 i는 구현의 편의를 위해 bitmask를 이용하여 하나의 정수값으로 나타낼 수 있습니다. 아직 bitmask에 대해 잘 모른다면, [bitmask](https://www.codetree.ai/missions/9/problems/bit-calculation/introduction) 유형을 공부하시고나서 다시 이 설명을 읽는 것을 추천드립니다. 여기서는 3번을 시작으로 겹치지 않게 방문한 위치를 x1, x2,..., xk라 헀을 때 2^x1 + 2^x2 +... + 2^xk 값이 i가 됩니다.

![](https://contents.codetree.ai/problems/3454/images/introductions-555a9477-45e3-4def-bc06-9191dc115b89.png)

이제 여기서 점화식을 세우기 보다는 **뿌려지는 형태의 동적계획법** 을 진행해보려고 합니다. 보통의 동적계획법 문제는 점화식을 세워 작은 문제에 해당하는 이전 값들이 채워져있다는 가정 하에서 현재 상태에 해당하는 최적의 값을 계산하는 식으로 진행됩니다. 이러한 방식은 `이미 완성된 값을 가져오는 형태의 동적계획법` 입니다. 하지만 상황에 따라 가져와야 할 부분을 직관적으로 떠올리거나 정리하는 것이 어려운 경우가 더러 있습니다. 지금 이 문제에서는 점화식을 세워 가져오는 방법으로 진행하기보다는, **이미 값이 구해져있다는 가정 하에서 이 상태가 영향을 미치는 그 다음 상태를 찾아 값을 갱신해주는 식인** 뿌려지는 형태의 동적계획법을 진행해보려고 합니다.

`dp[i][j]` 값이 이미 구해져있다고 가정해보겠습니다. 이제 그 다음 위치로 k번 정점으로 간다고 한다면, 지금까지 방문한 상태의 bitmask 값은 $i + 2^k$ 가 되고 마지막 방문 위치는 k가 되기에 아래와 같이 아직 방문하지 않은 모든 정점에 대해 값을 갱신해주면 됩니다.

![](https://contents.codetree.ai/problems/3454/images/introductions-f297db53-788c-497c-a08a-df0ff00618e5.png)

초기조건은 3번 지점을 시작으로 하며 현재 3번 위치에 서있으며 지금까지의 이동거리가 0이므로 `dp[8(=1000)][3] = 0` 이 됩니다.

이제 점화식에 따라 값을 갱신하면 됩니다. 이때 dp는 특성상 더 작은 문제부터 값이 채워져야 하는 것이 중요합니다. 이를 쉽게 작성하기 위해서는 그저 i값을 0부터 전부 채워져 있는 값인 $2^4 - 1(=1111)$ 까지 1씩 증가하며 진행하면 됩니다. 그 이유는 i가 증가하는 순으로 bitmask를 확인하면 해당 bit보다 더 작은 케이스는 이미 다 고려가 되었음을 보장할 수 있기 때문입니다.

이제 순서대로 dp값을 채우는 과정을 살펴보면 아래와 같습니다.

![](https://contents.codetree.ai/problems/3454/images/introductions-09265ad9-b285-4960-97ee-ed777b7d0c34.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-4f50e6a6-8b41-4839-9fe2-201dbf111f89.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-8b97e0e6-3398-4eed-b48a-3b078946ea31.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-b0860ea4-a6f7-4afe-a068-4fa9f985ae73.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-82dff986-52c9-4bab-a95f-84b56def70ca.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-ab7fb3bb-d4c3-4af7-990f-491c30e6cc0a.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-5db0dca9-7c39-45be-8249-34c0c8f0c732.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-85e53ee1-d07e-4d89-8a1b-5e78c2cbe89e.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-b1dbdf32-b4a3-45c6-a8b5-6d111db713a9.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-af8e13ec-b800-4bac-bec0-539962f7cb0f.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-85503bfe-0ef2-4291-9a1f-dcc648d55ad4.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-449594d1-d40f-4875-b0bc-ab4b6dba8b91.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-5f260155-1637-4aff-9bff-d9f5afb0943d.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-36647666-3d95-4bdf-ab11-1ff89ce557c0.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-792d375c-aa65-46e9-b435-11dfebb4467d.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-84d1ebe6-d1fb-4d24-ba28-8a6dba26f910.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-6952d0c3-694c-4b2a-abad-9f2b6b785ba7.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-71d900bf-9fe3-4281-b340-f7c114fb81db.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-2c5fe335-68f3-4c9f-a5b5-bc39eb1dc745.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-b787bfdb-c3b3-410d-9864-a6489817b7d1.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-22051e6b-a386-40bc-a778-effd42a71145.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-d34120cb-64b4-4459-bd4c-257d9bbc4e23.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-7e1473e4-b9fe-43cc-92be-fb9c9d2e056b.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-1f1fd97a-93e0-4f26-b47e-bfc4280aecb4.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-cf3c1f46-b869-43d3-97f3-253fedcc8fb1.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-7852b3e2-e351-498a-bd24-74cfa6419f4d.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-138a0484-db4f-41fd-b734-5a5bbaf6e319.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-cac397d2-ce70-47d5-9684-1768d2d9d8a2.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-6e71bffa-09f7-4670-bf3e-6922f5b5e040.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-8b84bc37-ccf9-4b31-999c-c93210e948bb.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-e6ed8716-4fa3-42bb-b8f5-de0a2a7b29b0.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-9cf12b17-5007-4df8-ac4f-7bbb3ecc92d5.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-5cea3b95-6977-4541-997a-40128439e68c.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-9bd4a206-4a9e-4704-ba8a-dc18c96f3079.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-82d40f46-189a-44d3-a9a0-e63741aa28be.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-16427296-c24e-4c54-8988-085693b2967c.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-70abd0f4-ea0d-4dd4-bc6d-8c8fd1bcedf3.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-89e40c86-b43c-4016-8a57-aba9e33b70dd.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-2e6f057f-1fa0-4968-9845-ea173edebd40.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-289dcb5d-8ef7-4545-abf7-865543f60d39.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-7f6856a7-18ec-4d7a-bd7b-2b485a2d2c48.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-87cc8716-e46d-4d1c-b056-fb1b5f56fa37.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-65d572cc-743a-468c-a6e1-b0867999bdd1.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-d27fd82a-830a-4d5d-a4e3-e72edfc21ba7.png) ![](https://contents.codetree.ai/problems/3454/images/introductions-79e65354-1dc9-4058-aa3f-6ea4264051cd.png)

1 / 45

값을 채운 뒤 답은 모든 정점을 방문한 상태 중 가능한 최소 이동거리가 됩니다. 즉, 어디에서 끝나는지는 전혀 상관이 없는 문제이기에 $dp[2^4-1(=1111)][i]$ 값 중 최솟값이 답이 됩니다. 이 풀이에서 dp의 상태는 $O(2^N * N)$ 개 이며, 각 상태에 대해 그 다음 정점에 해당하는 곳을 탐색하기 위해 $O(N)$ 개를 보게 되므로 총 시간복잡도는 $O(2^N * N^2)$ 이 됩니다. n이 커질수록 백트래킹으로 구현했을 때의 $O(N!)$ 에 비해 훨씬 빠른 시간복잡도를 갖는 방법이라 할 수 있습니다.

이 문제의 풀이 관련 코드는 아래와 같습니다.

```python
import sys

INT_MAX = sys.maxsize

n = 4
dist = [
    [0, 1, 3, 4],
    [1, 0, 9, 5],
    [3, 9, 0, 6],
    [4, 5, 6, 0]
]

# dp[i][j] : 
# 3번을 시작으로 겹치지 않게 방문한 위치를
# x1, x2, ..., xk라 헀을 때 
# 2^x1 + 2^x2 + ... + 2^xk 값이 i이고 (bitmask된 정수값이 i)
# 그래서 현재 서 있는 위치가 j가 되었을 때
# 가능한 최소 이동거리
dp = [
    [0] * n
    for _ in range(1 << n)
]

# 최소 이동거리를 구하는 문제이기에
# 초기값으로 아주 큰 값을 넣어줍니다.
for i in range(1 << n):
    for j in range(n):
        dp[i][j] = INT_MAX

# 초기조건은
# 3번 지점을 시작으로 하며 현재 3번 위치에 서있으며
# 지금까지 이동한 거리가 0인 상태인
# dp[8][3] = 0이 됩니다.
dp[8][3] = 0

# 뿌려주는 방식의 dp를 진행합니다.
# dp[i][j]가 계산이 되어있다는 가정하에서
# 그 다음 상태값을 갱신합니다.
for i in range(1 << n):
    for j in range(n):
        # j번 지점을 방문한게 정의상 불가능 하다면
        # 패스합니다.
        if ((i >> j) & 1) == 0:
            continue

        # 현재 j번에서 그 다음 위치로 k번 지점을 가게 되는 경우
        # 상태값을 계산하여 최솟값을 갱신해줍니다.
        for k in range(n):
            # k번 지점을 이미 방문한 적이 있다면
            # 중복 방문은 조건상 불가하므로 패스합니다.
            if ((i >> k) & 1) == 1:
                continue
            
            # j번에서 k번으로 가는 길이 없다면
            # 패스합니다.
            if dist[j][k] == 0:
                continue
            
            dp[i + (1 << k)][k] = min(
                dp[i + (1 << k)][k], dp[i][j] + dist[j][k]
            )

# 어디서 끝나던 상관이 없기 때문에
# 모든 지점을 방문한 경우 중 최솟값을 갱신합니다.
ans = INT_MAX
for i in range(n):
    # 최솟값을 갱신합니다.
    ans = min(ans, dp[(1 << n) - 1][i])

print(ans)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.