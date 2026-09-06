---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-board-and-words/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 4. Trie

## 보드판과 단어

Medium

60XP

평균 84분

57% 정답률

총 제출 57회

$n$ 개의 단어와 4x4 크기의 보드판이 주어집니다. 보드판의 각 칸에는 하나의 소문자 알파벳이 적혀있고, 주어지는 $n$ 개의 단어는 전부 소문자 알파벳으로 이루어져 있습니다.

보드판의 특정 위치에서 시작하여 인접한 8방향으로만 이동하는 것을 반복하여 방문하게 되는 칸에 있는 문자들을 순서대로 나열하여 만들 수 있는 문자열 중 입력으로 주어진 $n$ 개의 단어와 일치하는 경우를 찾아보려고 합니다. 단, 문자열을 만들 때 보드에서 같은 칸을 여러 번 방문해서는 안됩니다.

주어진 $n$ 개의 단어 중 보드를 이용하여 만들어 낼 수 있는 단어들을 찾고, 그 중 가장 길이가 긴 단어를 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $n$ 이 주어집니다.

두 번째 줄에는 $n$ 개의 단어가 공백을 사이에 두고 주어집니다.

세 번째 줄 부터는 4개의 줄에 걸쳐 보드판의 상태가 주어집니다. 각 줄에는 각 행에 해당하는 4개의 문자가 공백없이 주어집니다.

### 제한 조건

- $1 \le n \le 300,000$
- $1 \le$ 각 단어의 길이 $\le 8$

### 출력

주어진 $n$ 개의 단어 중 보드를 이용하여 만들어 낼 수 있는 가장 긴 단어의 길이를 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
apple app banana
aeaa
alpa
aaap
aaaa
```

출력

```
5
```

### 예제 2

입력

```
3
apple app banana
aeaa
alpn
anap
baaa
```

출력

```
6
```

### 제한

• Time Limit: 2000 ms

• Memory Limit: 180 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!