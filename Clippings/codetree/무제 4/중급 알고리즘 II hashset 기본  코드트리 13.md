---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-connected-vertex-2/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Disjoint Set (Union Find)

## 연결된 정점 2

Easy

30XP

평균 24분

58% 정답률

총 제출 189회

무수히 많은 정점을 가진 그래프가 있습니다. 초기에, 이 그래프는 간선을 가지고 있지 않습니다.

다음과 같은 질의가 $N$ 개 주어집니다.

- $a\ b$: 그래프에서 $a$ 번 정점과 $b$ 번 정점을 간선으로 잇습니다. 이후, $a$ 번 정점이 속한 연결 컴포넌트의 크기를 출력합니다.

연결 컴포넌트의 크기란, 간선으로 연결된 정점의 개수를 뜻합니다.

$N$ 개의 질의를 차례대로 수행하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 정수 $N$ 이 주어집니다.

그다음 줄부터 $N$ 개의 줄에 걸쳐, 두 정점의 번호를 나타내는 두 정수 $a$ 와 $b$ 가 공백으로 구분되어 주어집니다.

### 제한 조건

### 출력

두 개의 정점이 주어질 때 마다, 간선으로 연결한 후에 주어진 두 정점에서 간선으로 연결되어있는 모든 정점의 개수를 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
1 2
2 3
3 4
```

출력

```
2
3
4
```

### 예제 2

입력

```
3
1 2
3 4
1 4
```

출력

```
2
2
4
```

### 제한

• Time Limit: 2000 ms

• Memory Limit: 100 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!