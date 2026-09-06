---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-graphs-and-trees/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. 트리

## 그래프와 트리

Medium

60XP

평균 25분

57% 정답률

총 제출 288회

입력으로 무방향 그래프가 주어집니다. 이 그래프는 연결 그래프가 아닐 수 있습니다. 다시 말해서, 여러 개의 연결 요소로 이루어져 있을 수 있습니다.

여기서 연결 요소는 (1) 모든 정점이 서로 연결되어 있는 정점의 부분집합이며 (2) 이 연결 요소에 포함되는 정점들은 외부 정점들과 연결되어서는 안됩니다.

트리는 다음 조건을 만족하는 연결 요소입니다. 셋 중 하나만 만족해도 나머지를 만족하게 됩니다.

- 사이클이 없습니다.
- 정점이 $N$ 개이면, 간선이 $N - 1$ 개 있습니다
- 임의의 두 정점에 대해서 경로가 유일합니다.

이 그래프상의 연결 요소 중, 트리에 해당하는 것의 개수를 세는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 정점의 개수 $N$, 간선의 개수 $M$ 이 주어집니다.

두 번째 줄부터 $M+1$ 번째 줄에 각각 걸쳐 간선으로 연결된 두 개의 노드가 공백을 두고 차례대로 주어집니다. 주어지는 노드의 번호는 $1$ 에서 $N$ 사이입니다.

### 제한 조건

- $2 \le N \le 500$
- $1 \le M \le N(N-1)/2$
- $1 \le \texttt{주어지는 노드의 번호} \le N$

### 출력

주어진 그래프의 연결 요소 중 트리인 것의 개수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
6 3
1 2
2 3
3 4
```

출력

```
3
```

### 예제 2

입력

```
6 5
1 2
2 3
3 4
4 5
5 6
```

출력

```
1
```

### 예제 3

입력

```
6 6
1 2
2 3
1 3
4 5
5 6
6 4
```

출력

```
0
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!