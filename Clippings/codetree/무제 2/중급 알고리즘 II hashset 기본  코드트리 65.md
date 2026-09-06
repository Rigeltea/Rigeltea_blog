---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-reversing-g-and-h/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 상태 반전이 가능한 문제

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 구간 단위로 반전시키기

다음 문제를 생각해봅시다.

```
길이가 4인 문자열 0100이 주어졌을 때,
부분 문자열을 고르면, 해당 문자열 내 문자들이 
0 -> 1, 1 -> 0 이렇게 반전이 일어난다고 합니다.
부분 문자열을 적절하게 골라 최소 횟수로 문자열이 1111이 되도록 해보세요.
 

예로 0100에서 [2, 2] 구간을 잡아 0000을 만든 뒤,
[1, 4] 구간을 잡으면 전부 1111이 되므로 최소 횟수는 2가 됩니다.
```

이 문제는 어떻게 접근해 볼 수 있을까요?

이렇게 생각을 해봐야 합니다.

```
전부 숫자 1을 만들기 위해 뒤집어야 하는 구간 끼리는 어떤 관계가 있을까?
```

문제 특성상, 두 구간이 겹치는 곳에 있는 문자들은 2번 뒤집히기 때문에 결국 뒤집히지 않은 것과 같습니다.

즉, 이런 생각을 해볼 수 있습니다.

```
2번 뒤집혔다는 것은, 뒤집지 않았다는 것과 같다.
이는 곧, 뒤집을 필요가 없다는 말과도 같다.
```

예를 들어 다음과 같이 2번에 걸쳐 뒤집어 전부 숫자 1을 만드는 경우가 있을 수 있습니다.

![](https://contents.codetree.ai/problems/830/images/introductions-28eb6c89-74da-4d4c-b125-cd3a28ed1b2c.png)

하지만 이 과정은 겹치는 부분을 제외한 다른 두 구간을 뒤집는 것으로도 가능합니다.

![](https://contents.codetree.ai/problems/830/images/introductions-c7b3c07c-e2ff-41d1-86b0-e2836c0ed3ee.png)

따라서 겹치는 두 구간은 항상 겹치지 않게 풀 수 있고, 이 말은 즉 어떤 최적의 방법이 있을 때 겹치는 두 구간을 푸는 방식을 반복하여 모든 구간이 겹치지 않으며 뒤집는 구간의 수는 동일한 경우를 만들 수 있다는 뜻입니다. 겹치지 않는 구간을 잡아 전부 숫자 1을 만들어야 하는 문제를 풀기 위한 최적의 답은 **연속된 0으로 이루어진 서로 다른 그룹의 수** 와 같으므로, 비교적 쉽게 문제 해결이 가능해집니다.

이처럼 구간 단위로 뒤집는 문제의 경우, 구간을 겹쳐서 해결해야 할 이유가 없음을 이해하면 문제를 간단히 해결할 수 있습니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.