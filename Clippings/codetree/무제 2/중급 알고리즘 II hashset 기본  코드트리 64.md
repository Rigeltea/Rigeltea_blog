---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-do-not-overlap-the-meeting-room/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Greedy Algorithm

## 회의실 겹치지 않게 하기

Easy

20XP

평균 17분

75% 정답률

총 제출 341회

하나의 회의실이 있고, $N$ 개의 회의 요청이 들어왔습니다. 각 회의의 시작 시간과 끝 시간이 주어져 있으며, 한 회의가 시작되면 도중에 그만둘 수 없고, 한 회의가 끝나는 직후에 동시에 다른 회의가 시작될 수 있습니다. 이때 회의실은 하나밖에 없기 때문에 취소하는 회의 개수를 최소화하여 원활하게 진행할 수 있는 회의의 수를 최대로 하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 회의 요청이 들어온 횟수 $N$ 이 주어집니다.

두 번째 줄부터는 $N$ 개의 줄에 걸쳐 회의의 정보 $(s,\ e)$ 가 한 줄에 하나씩 공백을 사이에 두고 주어집니다. 이 의미는 해당 회의가 시간 $s$ 에서 시작하여 시간 $e$ 에 끝남을 의미합니다. 여기서 시간은 편의상 하나의 정수값으로 주어집니다.

### 제한 조건

- $1 \le N \le 100\,000$
- $0 \le \texttt{주어지는 시간} \le 100\,000$

### 출력

첫 번째 줄에 최대한 많은 수의 회의가 원활하게 진행되기 위해 취소해야 하는 최소 회의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
7
0 1
1 9
8 23
2 3
3 4
7 8
4 6
```

출력

```
1
```

예제 설명

접기

$[1,\ 9]$ 만 제외하면 남은 모든 회의를 원활하게 진행할 수 있게 됩니다. 이보다 더 많은 회의가 진행되도록 할 수는 없습니다.

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!