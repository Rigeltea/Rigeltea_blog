---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-reversing-g-and-h-3/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 상태 반전이 가능한 문제

## G & H 반전시키기 3

Medium

60XP

평균 26분

54% 정답률

총 제출 280회

'G', ‘H' 로만 이루어져 있는 길이가 $N$ 인 초기 문자열과 원하는 목표 문자열이 주어졌을 때, 구간을 최소 횟수로 잡아 해당 구간에 있는 문자를 'G' $\to$ 'H', 'H' $\to$ 'G'로 반전시켜 원하는 목표 문자열이 나오도록 하는 프로그램을 작성해보세요. 단, 한번에 뒤집을 수 있는 구간의 최대 크기는 $4$ 입니다.

### 입력

첫 번째 줄에는 $N$ 이 주어집니다.

두 번째 줄에는 길이가 $N$ 인 초기 문자열이 주어집니다.

세 번째 줄에는 길이가 $N$ 인 목표 문자열이 주어집니다.

### 제한 조건

- $1\le N\le 1\,000$
- 문자열은 'G', 'H'로만 이루어져 있습니다.

### 출력

초기 문자열이 목표 문자열이 되기 위해 잡아야 하는 최소 구간의 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
7
GHHHGHH
HGGGHHH
```

출력

```
2
```

예제 설명

접기

시작은 `GHHHGHH` 입니다.

여기서 처음 구간 $[3,\ 5]$ 를 잡으면 해당 구간의 문자들은 반전되어 `GHGGHHH` 가 됩니다.

이후 구간 $[1,\ 2]$ 을 잡아 반전시키면 목표 문자열은 `HGGGHHH` 를 얻게 됩니다.

크기가 $4$ 이하인 구간을 $2$ 개 보다 적게 사용해서는 목표 문자열을 만들 수 없습니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!