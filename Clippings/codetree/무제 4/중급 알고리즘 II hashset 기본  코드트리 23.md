---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-renumbering-process/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Topological Sort

## 새로 번호 매기기

Hard

90XP

평균 180분

46% 정답률

총 제출 80회

$n$ 개의 노드와 $m$ 개의 간선으로 이루어진 단방향 그래프가 주어졌을 때, 각 노드에 번호를 새로 매기려고 합니다. 새로 번호가 매겨진 이후에는 다음 규칙을 만족해야만 합니다.

- $x \to y$ 로 가는 간선이 있다면, $x$ 노드의 새로운 번호는 $y$ 노드의 새로운 번호보다 작아야만 합니다.
- 번호는 $1$ 번부터 $n$ 번까지 정확히 한 번씩만 등장해야 합니다.

조건을 만족하도록 번호를 새로 매겨주는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $n$ 과 $m$ 이 공백을 사이에 두고 주어집니다.

두 번째 줄 부터는 $m$ 개의 줄에 걸쳐 간선의 정보 $(x, y)$ 가 공백을 사이에 두고 주어집니다. 이는 $x$ 에서 $y$ 로 가는 간선이 존재함을 의미합니다.

### 제한 조건

### 출력

첫 번째 줄에 처음 주어진 노드 $1$ 번부터 $n$ 번까지 순서대로 각각 어떤 번호로 변경되었는지를 공백을 사이에 두고 출력합니다. 만약 가능한 답이 여러 개라면 사전순으로 가장 앞선 답을 출력하며, 가능한 답이 없다면 $-1$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
4 4
2 3
3 4
3 1
4 1
```

출력

```
4 1 2 3
```

### 예제 2

입력

```
4 3
2 3
3 4
3 1
```

출력

```
3 1 2 4
```

### 예제 3

입력

```
4 4
1 2
2 3
3 4
4 1
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