---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-node-best-count-2/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. Tree DP

## 노드 최적의 개수 2

Medium

60XP

평균 55분

42% 정답률

총 제출 194회

$1$ 번부터 $N$ 번까지 $N$ 개의 정점으로 이루어진 트리가 주어집니다.

여러분은 이 트리의 몇몇 정점에 물건을 놓으려고 합니다. 이미 $M$ 개의 정점에는 물건이 놓여 있으며, 최종적으로 모든 간선에 대해 그 간선이 잇는 두 정점 중 적어도 하나에는 물건이 놓여 있어야 합니다.

조건을 만족하기 위해 추가적으로 놓아야 하는 물건의 최소 개수를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 정점의 수 $N$ 과 처음에 이미 물건이 놓여 있는 정점의 수 $M$ 이 공백으로 구분되어 주어집니다.

그다음 줄부터 $N-1$ 개의 줄에 걸쳐, 한 줄에 간선 하나씩, 각 간선이 연결하는 두 정점의 번호가 공백으로 구분되어 주어집니다.

그다음 줄에 이미 물건이 놓여 있는 $M$ 개의 정점의 번호가 공백으로 구분되어 주어집니다.

### 제한 조건

- $2 \le N \le 100\,000$
- $1 \le M \le N$
- $1 \le \texttt{간선이 연결하는 정점 번호} \le N$
- 이미 물건이 놓여 있는 $M$ 개의 정점의 번호는 서로 다릅니다.
- 주어지는 그래프는 트리입니다.

### 출력

첫 번째 줄에 조건을 만족하기 위해 추가로 필요한 최소 물건의 수를 출력하세요.

### 입력 예제

### 예제 1

입력

```
3 1
1 2
1 3
1
```

출력

```
0
```

### 예제 2

입력

```
4 1
1 2
1 3
1 4
2
```

출력

```
1
```

### 예제 3

입력

```
6 1
1 2
2 3
3 4
4 5
4 6
3
```

출력

```
2
```

### 예제 4

입력

```
6 3
1 2
2 3
3 4
4 5
4 6
1 5 6
```

출력

```
1
```

### 제한

• Time Limit: 3000 ms

• Memory Limit: 400 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!