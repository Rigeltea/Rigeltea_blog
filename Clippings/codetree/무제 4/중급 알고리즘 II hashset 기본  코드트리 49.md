---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-selection-of-representatives/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. Bitmask DP

## 대표 선발

Hard

90XP

평균 87분

79% 정답률

총 제출 29회

$100$ 명의 사람이 있습니다. 각 사람에게는 $1$ 번부터 $100$ 번까지 번호가 붙여져 있습니다. $n$ 개의 그룹이 있으며, 한 사람이 여러 그룹에 속할 수 있습니다. 각 그룹마다 대표를 한 명씩 선발하되, 한 사람이 여러 그룹의 대표가 되지 않도록 선발할 수 있는 경우의 수를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 그룹의 수를 의미하는 $n$ 이 주어집니다.

두 번째 줄 부터는 $n$ 개의 줄에 걸쳐 그룹 정보가 주어집니다. 그룹 정보는 $m$ $c_1$ $c_2$ $\cdots$ $c_m$ 형태로 공백을 사이에 두고 주어집니다. $m$ 은 그룹에 속하는 사람의 수, 그리고 $c_1$ 부터 $c_m$ 까지는 해당 그룹에 속하는 사람들의 번호를 의미합니다.

### 제한 조건

### 출력

사람이 겹치지 않도록 모든 그룹에 대해 대표를 선발할 수 있는 서로 다른 가짓수를 10,007로 나눈 나머지를 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
3 1 2 5
2 2 5
1 1
```

출력

```
2
```

### 예제 2

입력

```
3
3 1 2 5
3 3 4 5
2 5 6
```

출력

```
12
```

### 제한

• Time Limit: 5000 ms

• Memory Limit: 288 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!