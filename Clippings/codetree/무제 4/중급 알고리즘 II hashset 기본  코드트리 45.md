---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-number-of-non-overlapping-pairs/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Bitmask

## 겹치지 않는 쌍의 수

Easy

30XP

평균 20분

77% 정답률

총 제출 112회

$30$ 명의 사람이 있습니다. 각 사람에게는 $1$ 번부터 $30$ 번까지 번호가 붙여져 있습니다. $N$ 개의 그룹이 있으며, 한 사람이 여러 그룹에 속할 수 있습니다. 서로 다른 두 그룹을 잡았을 때 단 한 사람도 동시에 두 그룹에 속하지 않는 경우의 수를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 그룹의 수를 의미하는 $N$ 이 주어집니다.

두 번째 줄부터는 $N$ 개의 줄에 걸쳐 그룹 정보가 주어집니다. 그룹 정보는 $m\ c_1\ c_2\ \cdots\ c_m$ 형태로 공백을 사이에 두고 주어집니다. $m$ 은 그룹에 속하는 사람의 수이며, $c_1$ 부터 $c_m$ 까지는 해당 그룹에 속하는 사람들의 번호를 의미합니다.

### 제한 조건

### 출력

두 그룹을 잡았을 때 서로 겹치는 사람이 없는 경우의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
4
2 1 30
3 5 2 9
3 1 3 5
2 4 30
```

출력

```
3
```

예제 설명

접기

첫 번째 예제에서 (그룹 1, 그룹 2), (그룹 2, 그룹 4), 그리고 (그룹 3, 그룹 4)를 잡았을 경우에만 겹치는 사람이 없으므로 답은 3이 됩니다.

### 예제 2

입력

```
4
2 1 30
3 5 2 9
3 1 3 5
3 4 30 5
```

출력

```
1
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!