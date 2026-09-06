---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-height-of-friends-3/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Topological Sort

## 친구의 키 3

Easy

30XP

평균 16분

76% 정답률

총 제출 80회

$n$ 명의 친구가 키가 큰 사람부터 내림차순으로 순서대로 서있습니다. 이때 $n$ 명의 친구는 모두 키가 다르며, 어떤 순서로 서있는지에 대한 단서로 $m$ 개의 정보가 주어집니다. 각 정보는 $(a, b)$ 형태로 주어지며, 이는 $a$ 번 친구가 $b$ 번 친구보다 키가 크다는 것을 의미합니다. 친구들이 서있는 순서를 앞에서부터 차례대로 구해주는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $n, m$ 이 공백을 사이에 두고 주어집니다.  
두 번째 줄부터는 $m$ 개의 줄에 걸쳐 두 사람의 키에 대한 정보 $(a, b)$ 가 공백을 사이에 두고 주어집니다. 이는 $a$ 번 친구가 $b$ 번 친구보다 키가 크다는 것을 의미합니다.

### 제한 조건

### 출력

친구들이 서있는 순서를 앞에서부터 차례대로 공백을 사이에 두고 출력합니다. 단 만약 그러한 조건을 만족하는 것이 불가능하다면 -1을, 답이 여러 개라면 사전순으로 가장 앞선 답을 출력하도록 합니다.

### 입력 예제

### 예제 1

입력

```
5 5
3 2
1 5
2 1
3 4
4 2
```

출력

```
3 4 2 1 5
```

### 예제 2

입력

```
5 4
3 2
1 5
2 1
3 4
```

출력

```
3 2 1 4 5
```

### 예제 3

입력

```
5 5
3 2
1 5
2 1
4 2
5 2
```

출력

```
-1
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!