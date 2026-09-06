---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-change-tree-traversal/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 이진 트리와 탐색

## 트리 순회법 변경

Hard

90XP

평균 12분

65% 정답률

총 제출 257회

이진 검색 트리는 모든 노드에 대해서, 다음과 같은 두 가지 조건을 만족하는 이진 트리입니다.

- 왼쪽 서브트리에 있는 모든 노드의 값은 현재 노드의 값보다 작다.
- 오른쪽 서브트리에 있는 모든 노드의 값은 노드의 값보다 크다.

이진 검색 트리를 전위 순회한 결과가 주어졌을때, 이 트리를 후위 순회한 결과를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 노드의 개수 $N$ 이 주어집니다.

두 번째 줄부터 트리를 전위순회한 결괏값이 매 줄에 걸쳐 차례대로 주어집니다.

### 제한 조건

- $1 \le N \le 10\,000$
- $1 \le \texttt{노드 값} \le 1\,000\,000$
- 노드 값에는 중복이 없습니다.

### 출력

입력으로 주어진 이진 트리를 후위 순회한 결과를 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
9
6
4
2
1
3
5
9
7
8
```

출력

```
1
3
2
5
4
8
7
9
6
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!