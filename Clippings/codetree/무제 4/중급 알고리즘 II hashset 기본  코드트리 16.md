---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-delete-edge/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Kruskal

## 간선 제거하기

Easy

30XP

평균 11분

91% 정답률

총 제출 68회

$N$ 개의 정점과 $M$ 개의 간선이 있는 그래프가 있습니다.

주어진 그래프에서 간선을 적절히 빼서 모든 정점이 연결되어 있는 상태는 유지하되 간선의 가중치를 최대한 많이 지우고 싶습니다.

모든 정점이 연결되어 있는 상태를 유지하면서 뺄 수 있는 간선의 가중치의 최대를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 정점의 개수 $N$, 간선의 개수 $M$ 이 공백을 두고 주어집니다.

두 번째 줄부터 $M$ 개의 줄에 걸쳐, 각 간선의 양 끝 점과 가중치가 공백을 두고 주어집니다.

### 제한 조건

- $1 \le N \le 100\,000$
- $N-1 \le M \le 100\,000$
- $1 \le \texttt{가중치} \le 10\,000$

### 출력

모든 정점이 연결되어 있는 상태를 유지하면서 뺄 수 있는 간선의 가중치의 최대를 출력합니다.

### 입력 예제

### 예제 1

입력

```
5 6
1 2 50
1 3 10
2 3 40
1 4 30
3 5 20
4 5 15
```

출력

```
80
```

### 예제 2

입력

```
5 4
1 2 1
2 3 1
3 4 1
4 5 1
```

출력

```
0
```

### 제한

• Time Limit: 2000 ms

• Memory Limit: 100 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!