---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-rock-paper-scissors-to-see-the-future/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. LR Technique

## 미래가 보이는 가위바위보

Easy

40XP

평균 49분

64% 정답률

총 제출 628회

$A$ 와 $B$ 가 가위바위보를 총 $N$ 회 진행합니다. $A$ 는 $B$ 가 무엇을 낼지 알고 있습니다. $A$ 는 주먹, 가위, 보자기 중 같은 것을 연속해서 내고, 게임 $N$ 회 중 최대 한 번만 자신이 내는 것을 바꿔, 이후에는 바꾼 것을 계속 내려고 합니다. 예를 들어 $K$ 번 연속 주먹을 내고, $N-K$ 번은 가위를 냅니다. $A$ 가 이길 수 있는 게임 수의 최댓값을 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에 $N$ 이 주어집니다.

두 번째 줄부터 $N$ 개의 줄에 걸쳐 각 줄에 주먹, 가위, 보자기 중 $B$ 가 무엇을 내는지에 대한 정보가 주어집니다. $H$ 는 주먹, $S$ 는 가위, $P$ 는 보자기를 나타냅니다.

### 제한 조건

- $1 \le N \le 100\,000$
- 주어지는 문자열은 $H$, $S$, $P$ 로만 구성되어 있습니다.

### 출력

첫 번째 줄에 $A$ 가 이길 수 있는 게임 수의 최댓값을 출력합니다.

### 입력 예제

### 예제 1

입력

```
5
P
P
H
P
S
```

출력

```
4
```

예제 설명

접기

$1$ 부터 $4$ 회까지 가위를 내고 마지막 판에 주먹을 내면 $3$ 번째 판 빼고 모든 판을 이길 수 있습니다. $A$ 가 이보다 더 많이 이길 수 있는 방법은 없습니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!