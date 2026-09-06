---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-reversing-g-and-h-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 상태 반전이 가능한 문제

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 앞을 전부 반전시키기

다음 문제를 생각해봅시다.

```
길이가 5인 문자열 11000이 주어졌을 때,
특정 위치를 선택하면, 해당 위치를 포함하여 앞에 있는 모든 문자에 대해
0 -> 1, 1 -> 0 이렇게 반전이 일어난다고 합니다.
최소 횟수로 선택을 진행하여 문자열이 11111이 되도록 해보세요.
 
예로 11000에서 처음 2번째 칸을 선택하여 00000을 만든 뒤,
5번째 칸을 선택하면 11111이 되므로 최소 횟수는 2가 됩니다.
```

이 문제는 어떻게 접근해 볼 수 있을까요?

먼저 이 생각을 해봐야 합니다.

```
같은 칸을 두 번 이상 선택하는게 의미가 있을까?
```

이 문제에서는 **같은 칸을 두 번 이상 선택하는게 전혀 의미가 없습니다**. 왜냐하면 2번을 선택하는 것은 선택을 하지 않는 것과 정확히 일치하기 때문이죠.

또 이런 생각도 해볼 수 있습니다.

```
각 칸에 영향을 끼치는 위치는 어디일까?
```

다섯 번째 위치를 먼저 살펴보면, 다섯 번째 위치만이 영향을 끼칠 수 있습니다. 따라서 만약 **다섯 번째 위치가 0이라면 다섯 번째 위치는 꼭 선택되어** 해당 위치를 1로 만들어 줘야만 합니다.

![](https://contents.codetree.ai/problems/887/images/introductions-e290a249-50a5-4d02-8aff-2aa207ef0bc8.png)

네 번째 위치는 어디에 영향을 받을까요? 뒤에 위치들을 누를지 말지는 이미 고려가 되었으므로, 이제는 네 번째 위치에만 영향을 받게 됩니다. 따라서 만약 **네 번째 위치가 0이라면 네 번째 위치는 꼭 선택되어** 해당 위치를 1로 만들어 줘야 합니다. 반대로, 이번 경우에는 네 번째값이 이미 1이기 때문에 네 번째 위치는 절대로 선택 되어서는 안됩니다.

![](https://contents.codetree.ai/problems/887/images/introductions-576e3d13-b490-46ed-8dfc-61dd14d27203.png)

세 번째 위치는 이제 세 번째 위치에만 영향을 받게 됩니다. 하지만 세 번째 값은 이미 1이기 때문에 선택되지 않습니다.

![](https://contents.codetree.ai/problems/887/images/introductions-95daad2b-a3af-4d37-aaa2-e2cea38ad2a7.png)

두 번째 위치는 이제 두 번째 위치에만 영향을 받게 됩니다. 두 번째 값은 0이기 때문에 꼭 선택되어야 하므로 눌러줍니다.

![](https://contents.codetree.ai/problems/887/images/introductions-8f583fc6-9c72-4200-a04a-4b7d09098274.png)

첫 번째 위치는 이제 첫 번째 위치에만 영향을 받게 됩니다. 하지만 첫 번째 값은 이미 1이기 때문에 선택되지 않습니다.

이렇듯 선택에 의해 앞에 있는 모든 값들이 반전되는 문제의 경우에는, **뒤에서 부터** 순차적으로 진행하며 꼭 눌려야만 하는 위치를 판단하는 식으로 문제를 해결할 수 있습니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.