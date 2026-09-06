---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-reserve-hotel/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. +1-1 technique

## 호텔 예약

Easy

20XP

평균 30분

46% 정답률

총 제출 690회

$N$ 명의 사람이 동일한 호텔에 투숙을 하는데, $i$ 번째 사람은 $s_i$ 날에 들어와서 $e_i$ 날에 나가게 됩니다. 서로 다른 사람끼리 같은 방을 쓸 수 없다 했을 때 $N$ 명의 예약을 문제 없이 처리하기 위해 필요한 최소 방의 수를 구하는 프로그램을 작성해보세요. 단, 한 사람이 나가는 날과 다른 사람이 들어오는 날이 일치하는 경우 두 사람은 같은 방에 머무를 수 없다고 가정합니다.

### 입력

첫 번째 줄에는 $N$ 이 주어집니다.  
두 번째 줄 부터는 $N$ 개의 줄에 걸쳐 i번째 사람에 해당하는 $s_i$, $e_i$ 정보가 공백으로 구분되어 주어집니다.

### 제한 조건

### 출력

문제 없이 모든 예약을 받기 위해 필요한 최소 방의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
1 3
3 5
4 5
```

출력

```
2
```

예제 설명

접기

$2$ 번째 사람과 $3$ 번째 사람이 같은 날에 예약이 되어있고, 그 외에 예약이 겹치는 날짜는 없기 때문에, 필요한 방의 최소 개수는 $2$ 개입니다.

![](https://contents.codetree.ai/problems/2201/images/problems-cb97c854-4ae5-424f-aafc-76a78d74543a.png)

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!