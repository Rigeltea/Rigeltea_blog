---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-sum-of-n-natural-numbers/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Parametric Search

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 문제 조건에 맞게 Bound를 설정

다음 문제는 어떻게 해결해 볼 수 있을까요?

```
1부터 n까지의 자연수의 합이 100이상인 경우 중 
가능한 n의 최솟값을 구하는 프로그램을 작성해보세요.

단, 답은 1에서 30사이라고 가정합니다.
```

무작정 코드를 작성한다면, 1, 2, 3..., 30 전까지 계속 더해보며 최초로 그 합이 100을 넘는 순간을 찾아 바로 그 직전의 숫자를 구하게 될 것입니다. 넘어야 하는 합을 s라 했을 때 시간복잡도는 $O(S)$ 가 됩니다.

하지만 만약 이 문제가 수학 문제로 나왔다면, 다음과 같이 시도하게 될 것입니다.

1. 1차 시도 (n = 15)

1부터 15까지의 합은 120이므로, **일단 15은 답의 후보 중 하나입니다.**  
이제 더 작은 값도 가능한지 `[1 ~ 14]` 사이를 조사해보려고 합니다.

2. 2차 시도 (n = 7)

1부터 7까지의 합은 28이므로, **n은 분명히 7보다 커져야 합니다.**  
이제 더 좋은 경우가 있을지 `[8 ~ 14]` 사이를 조사해보려고 합니다.

3. 3차 시도 (n = 11)

1부터 11까지의 합은 66이므로, **n은 분명히 11보다 커져야 합니다.**  
이제 더 좋은 경우가 있을지 `[12 ~ 14]` 사이를 조사해보려고 합니다.

4. 4차 시도 (n = 13)

1부터 13까지의 합은 91이므로, **n은 13보다 커져야 합니다.**  
이제 `[14 ~ 14]` 사이를 조사해보면 됩니다.

5. 5차 시도 (n = 14)

1부터 14까지의 합은 105이므로, **14도 답의 후보 중 하나가 됩니다.**  
더 이상 탐색할 범위가 없으므로, 가능했던 후보 `15, 14` 중 최솟값인 14가 답이 됩니다.

이렇듯 5번 만에 문제에서 원하는 답을 구할 수 있게 됩니다. 이게 어떻게 가능한 걸까요?

잘 생각해보면, 이 문제는 n이 커질수록 1부터 n까지의 합이 커진다는 특성을 가지고 있습니다. 즉, x축을 n, y축을 1부터 n까지의 합이라고 했을 때 다음과 같은 그림이 만들어지게 됩니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-99c74e7a-5bc7-4d78-8e1f-41b40f19e9e7.png)

이 그림에서 조건을 만족하는 n들 중 (1부터 n까지의 합이 100 이상인 경우) 최솟값을 구해야 합니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-2355df11-4a68-4cd0-a15d-e0c2d4090707.png)

가능한 범위는 1에서 30 사이이므로 일단 전부 조건을 충족시킬 가능성이 있습니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-a62fab19-3766-4925-bed1-931aca201477.png)

먼저 n이 15이었을 때를 확인해봅니다. 1부터 15까지의 합은 120이므로 이미 조건을 만족하기 때문에, 조건을 만족하는 경우 중 최솟값을 구해야 하는 이 문제에서는 n이 16보다 큰 경우를 더 이상 탐색해야 할 필요가 없습니다. **따라서 n=15는 답의 후보가 되며, 그 다음 탐색 범위는 `[1, 14]` 가 됩니다.**

![](https://contents.codetree.ai/problems/1589/images/introductions-190ae84a-e206-4b96-90d7-f4de53f7fa59.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-81b7a25e-d859-4dfa-976d-ccd2bbfd162b.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-9f0731e9-8ef8-4b38-b91b-89419d4b06ca.png)

1 / 3

이제 n이 1과 14의 가운데 값인 7이었을 경우를 확인해봅니다. 1부터 7까지의 합은 28이므로 **n은 조건을 만족시키기 위해 분명히 7보다 커져야 합니다.** 따라서 7보다 작은 경우는 전부 버리게 되고, 그 다음 탐색 범위는 `[8 ~ 14]` 가 됩니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-f08d6072-9c8c-419d-bedf-76e14e4c30b0.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-52710f93-6626-438b-83e5-d1a5becf2ce1.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-2f36b648-6160-416f-b099-1c45dae033c0.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-34409e5f-2640-4fea-b6ae-9a15344e6985.png)

1 / 4

다음에는 n이 8과 14의 가운데 값인 11이었을 경우를 확인해봅니다. 1부터 11까지의 합은 66이므로 **n은 조건을 만족시키기 위해 분명히 11보다 커져야 합니다.** 따라서 11보다 작은 경우는 전부 버리게 되고, 그 다음 탐색 범위는 `[12 ~ 14]` 가 됩니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-95b7db04-880a-4320-9b20-686bab2910cd.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-68376d93-c42f-4592-964d-8822f81b64de.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-f8ac4821-88b6-4130-bd9c-114a11fd723c.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-81c54f12-cf3d-4722-a165-bae5ffcbe99b.png)

1 / 4

다음에는 n이 12과 14의 가운데 값인 13이었을 경우를 확인해봅니다. 1부터 13까지의 합은 91이므로 **n은 조건을 만족시키기 위해 분명히 13보다 커져야 합니다.** 따라서 13보다 작은 경우는 전부 버리게 되고, 그 다음 탐색 범위는 `[14 ~ 14]` 가 됩니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-216e926a-6248-4cf6-9492-a1844dc92ebb.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-387340ea-c4c8-4d3e-9454-ced5933ffabc.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-fe3390ed-4896-4c5b-aa5b-653003d0f48e.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-d264a6e0-00b0-4590-861a-6aad73999c42.png)

1 / 4

마지막으로 n이 14인 경우를 확인해봅니다. 1부터 14까지의 합은 105이므로, **14도 답의 후보 중 하나가 됩니다.**  
더 이상 탐색할 범위가 없으므로, 가능했던 후보 `15, 14` 중 최솟값인 14가 답이 됩니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-7cc05ffd-2b2c-436c-969c-005037c56c18.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-1a0f80d2-e0d8-433c-ad1c-e9f72278d89e.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-a997c25b-c3d2-4401-89db-c1ce7b37fce4.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-d7939ed6-e82d-470f-b887-715141c93a62.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-bfc3ebf4-c674-4696-8e84-5d4d83975189.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-46031b5e-a910-43ce-9384-0297c7fd3f83.png)

1 / 6

이처럼 답이 절대 될 수 없는 범위는 버리고, 답이 되는 범위에서는 가능한 답 중 문제에서 원하는 조건(여기서는 최솟값)에 맞는 답을 계속 찾아가주면 됩니다. 이러한 경우에는 이번 문제에서처럼 x 값이 증가함에 따라 y값이 같이 계속 증가하거나, 계속 감소하는 형태에서 **이진 탐색** 을 진행하여 문제에서 원하는 답을 구할 수 있습니다. 이렇게 답을 기준으로 이진탐색을 진행하는 방식을 Parametric Search 라고 부릅니다.

![](https://contents.codetree.ai/problems/1589/images/introductions-8a287282-4a70-4c00-81a4-425540b5e216.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-18328762-4925-4775-abe6-d0c36236ccd4.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-57382aec-fa35-4ed2-aaf1-2e5176b4f01e.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-9f0ba904-3fcf-4a02-97b5-3c650dc84ab2.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-08d08319-cf43-4345-97e5-10d6677e9f90.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-59dc8846-10ac-45b3-af4e-4e22d74ba0f0.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-36c1a8fc-07a7-45b4-b05a-ec0c228e3458.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-7ae21719-77c3-4908-a821-56aa4c4308b9.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-0f27ed62-4b8d-45b6-a20c-8fd31ed2c509.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-1118a989-1fdb-4f72-935b-5c2c36bf4e06.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-6c8484d5-4d38-418c-9654-ca94b53ad7b1.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-3024bd10-9ee8-41a7-bd41-a5795baed732.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-242ec6fe-c606-4c9d-aa9f-4c46fb036d17.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-472f31d3-3cf1-4372-9b21-fb35b55b20db.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-a3347d3a-5fed-40dc-bfeb-55ba03cf94bb.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-1db3ea34-b65d-4caa-a9dc-e9710bb825bc.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-82b6ea7b-0d94-40a8-88c5-aac36a6cea7d.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-38c43cbe-81f8-4b68-86bd-2ca324ab36ef.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-a353cd1f-e599-45b0-9ada-e418bffe8572.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-35907502-6609-4aca-908d-6c9cf806b47d.png) ![](https://contents.codetree.ai/problems/1589/images/introductions-d72e2cc6-25a8-4318-beda-0e1155fc23ca.png)

1 / 21

코드 개형은 다음과 같습니다. 이 문제에서 원하는 답은 **합이 100 이상인 경우 중 최솟값 입니다.** 따라서 최솟값을 구하기 위해서는 `min_num` 이라는 변수를 활용해 초기값으로 답이 될 수 없는 최댓값인 `31` 을 넣어놓고 문제를 해결합니다. 이는 [Lower Bound, Upper Bound](https://www.codetree.ai/missions/8/concepts/51/problems/number-of-integers/introduction) 를 계산하는 코드와 많이 유사합니다.

```python
left = 1                        
right = 30                      
min_num = 31                    

while left <= right:          
    mid = (left + right) // 2     
    if (1):
        (2)        
    else:
        (3)

print(min_num)
```

이제 min\_num 값이 갱신되는 순간이 언제인지를 생각해봅니다. min\_num은 정의상 **mid \* (mid + 1) / 2이 100보다 크거나 같은 경우** 에 대해 가능한 mid 값들 중 최솟값이 되어야 합니다.

따라서 (1) 위치에 `mid * (mid + 1) / 2 >= 100` 조건을 걸어줍니다. 왼쪽에 조건을 만족하는 mid값이 더 있을 수 있으므로 right값을 움직여줘야 하며, 이 경우 min\_num을 현재까지의 최솟값인 min\_num과 mid를 비교하여 둘 중 더 작은 값으로 넣어줘야 합니다. 이처럼 답의 후보가 되는 범위를 항상 **if 조건에** 넣어 처리한다는 생각으로 코드를 작성하시면 됩니다.

조건을 만족하지 않는 경우에는 left값을 움직여주면 됩니다. 따라서 코드는 다음과 같이 작성이 가능합니다.

```python
left = 1                             # 가장 작은 숫자 값을 설정합니다.
right = 30                           # 가장 큰 숫자 값을 설정합니다.
min_num = 31                         # 최소이므로, 답이 될 수 있는 값보다 더 큰 값으로 설정합니다.

while left <= right:                 # [left, right]가 유효한 구간이면 계속 수행합니다.
    mid = (left + right) // 2        # 가운데 위치를 선택합니다.
    if mid * (mid + 1) // 2 >= 100:  # 1부터 n까지의 합이 100보다 같거나 크다면
        right = mid - 1              # 왼쪽에 조건을 만족하는 숫자가 더 있을 가능성 때문에 right를 바꿔줍니다.
        min_num = min(min_num, mid)  # 답의 후보들 중 최솟값을 계속 갱신해줍니다.
    else:
        left = mid + 1               # 100보다 작은 경우라면 left를 바꿔줍니다.

print(min_num)                       # 조건을 만족하는 최소 n 값을 출력합니다.
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.