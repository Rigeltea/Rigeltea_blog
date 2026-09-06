---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-priority-construction/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. Graph DP

## 우선순위 건설

Easy

30XP

평균 18분

73% 정답률

총 제출 105회

$1$ 번부터 $N$ 번까지 $N$ 개의 건물을 건설하려고 합니다.

어떤 건물은 이전에 반드시 완공해야 하는 건물들이 있습니다. 즉, 이 필수 건물을 모두 짓고 난 후에 건물을 짓기 시작할 수 있습니다.

위의 조건을 만족한다면, 여러 개의 건물을 동시에 지을 수 있습니다.

각 건물을 완성하기까지 걸리는 최소 시간을 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 건물의 수 $N$ 이 주어집니다.

그 다음 줄부터 $N$ 개의 줄에 걸쳐, 각 건물을 짓는데 걸리는 시간을 나타내는 정수 $t$ 와, 그 건물을 짓기 위해 먼저 지어야 하는 건물의 번호를 나타내는 정수가 공백으로 구분되어 주어집니다. 각 줄 마지막엔 입력의 끝을 의미하는 $-1$ 이 주어집니다.

### 제한 조건

- $1 \le N \le 500$
- $1 \le t \le 100\,000$
- 각 건물에 대해, 그 건물을 짓기 위해 먼저 지어야 하는 건물의 번호는 서로 다릅니다.
- 조건에 따라, 모든 건물을 짓는 것이 가능합니다.

### 출력

첫 번째 줄부터 $N$ 개의 줄에 걸쳐, 각 건물을 완성하기까지 걸리는 최소 시간을 번호 순서대로 한 줄에 하나씩 출력합니다.

### 입력 예제

### 예제 1

입력

```
5
5 -1
4 3 -1
4 1 -1
2 2 1 -1
6 3 -1
```

출력

```
5
13
9
15
15
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!