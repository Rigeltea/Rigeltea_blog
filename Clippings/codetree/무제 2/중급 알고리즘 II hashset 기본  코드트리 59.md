---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-max-of-partial-sum-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Greedy Algorithm

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 연속 부분 합의 최댓값 구하기

다음 문제는 어떻게 해결할 수 있을까요?

```
다음과 같이 8개의 숫자가 주어졌을 때
특정 구간을 잡아 그 구간 내에 있는 숫자의 합이 최대가 되도록 해보세요.
[4, 3, -6, 9, -15, 1, 3, -2]
```

이 문제의 경우 양수와 음수가 섞여 있기 때문에 어디에서 시작하여 어디까지 구간을 잡아야 할지 금방 떠오르지 않습니다.

하지만 이렇게 생각해보면 어떨까요?

```
왼쪽에서부터 순서대로 구간을 확장해 나가다가 
끊어야 하는 순간이 온다면, 그건 과연 언제일까요?
```

`4, 3` 이렇게 구간이 잡혔을 때 합은 7이고, 3번째 숫자인 -6이 더해졌더라도 여전히 합은 1(양수)이기 때문에 뒤에 숫자를 더 추가했을 때 합이 더 커질 가능성이 있습니다.

하지만 `4, 3, -6, 9, -15` 까지 확장되는 순간 합은 -5(음수)가 되었기 때문에,  
이후 6번째 원소 입장에서 봤을 때는 **여기서 끊고 6번째 원소부터 새로 시작하는 것이 더 좋습니다.**

따라서 이 문제는 왼쪽에서부터 순서대로 수를 보며 구간을 확장하다가, 합이 0보다 작아지는 순간 구간 확장을 멈추고 그 다음 원소부터 구간을 다시 만들어가는 그리디 알고리즘을 적용할 수 있습니다.

![](https://contents.codetree.ai/problems/2228/images/introductions-e5834a3a-2ff4-4304-9448-5c71cf9999b9.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-306814f0-9802-4fdd-b991-a70b3aa3c1fd.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-f1a0a512-0bb3-466b-b367-b8ad7c84d4f0.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-feed5148-1b1b-4ea8-89dd-079b82fdb722.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-cfe99d58-476e-4797-9561-0f6a08abffcb.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-e75699e9-131b-412d-8bea-264f514236b9.png) ![](https://contents.codetree.ai/problems/2228/images/introductions-b551c6da-8cd1-4f6c-83a0-ed976fc3d1f0.png)

1 / 7

이렇게 순차적으로 진행하며 합을 계산하고, 그중 최댓값을 구하면 됩니다. 이 방법의 시간 복잡도는 $O(N)$ 이 됩니다.

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.