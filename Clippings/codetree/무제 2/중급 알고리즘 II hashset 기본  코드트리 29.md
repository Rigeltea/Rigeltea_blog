---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-max-rect-sum-in-grid/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Prefix Sum

## 최대 직사각형 합

Hard

90XP

평균 156분

37% 정답률

총 제출 756회

$-1\,000$ 이상 $1\,000$ 이하의 숫자로만 이루어진 $N \times N$ 크기의 $2$ 차원 격자 상태가 주어졌을 때, 격자를 벗어나지 않는 직사각형 하나를 적절하게 잡아 사각형 내 숫자들의 합이 최대가 되도록 하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ 이 주어집니다.

두 번째 줄 부터는 $N$ 개의 줄에 걸쳐 각 행에 해당하는 $N$ 개의 숫자가 공백을 두고 차례대로 주어집니다.

### 제한 조건

- $1 \le N \le 300$
- $-1\,000 \le 원소의 크기 \le 1\,000$

### 출력

격자를 벗어나지 않는 직사각형 중 사각형 내 숫자들의 합이 최대가 되는 경우의 합을 출력합니다.

### 입력 예제

### 예제 1

입력

```
3
1 2 3
6 -900 7
7 7 9
```

출력

```
23
```

예제 설명

접기

다음과 같이 범위를 잡으면 합이 $23$ 으로 최대가 됩니다.

1 2 3

6 -900 7

**7 7 9**

### 제한

• Time Limit: 3000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!