---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-substring-occurrence-count-3/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. KMP

## 부분 문자열 등장 횟수 3

Easy

30XP

평균 15분

85% 정답률

총 제출 41회

소문자 알파벳으로만 이루어진 문자열 $T$ 와 문자열 $P$ 가 주어졌을 때, 문자열 $P$ 를 문자열 $T$ 에서 부분 문자열로서 겹치지 않게 최대 몇 번 고를 수 있는지를 판단하는 프로그램을 작성해보세요. 여기서 부분 문자열이란 연속하여 나올 수 있는 문자열을 의미합니다.

### 입력

첫 번째 줄에 문자열 $T$ 가 주어집니다.

두 번째 줄에 문자열 $P$ 가 주어집니다.

문자열 $T$ 와 문자열 $P$ 는 소문자 알파벳으로만 이루어져 있습니다.

### 제한 조건

- $1\le \texttt{문자열}\ T \texttt{의 길이}, \texttt{문자열}\ P \texttt{의 길이} \le100\,000$
- 문자열 $T$ 와 문자열 $P$ 는 소문자 알파벳으로만 이루어져 있습니다.

### 출력

문자열 $T$ 에서 문자열 $P$ 를 부분 문자열로서 겹치지 않게 최대로 고를 수 있는 횟수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
ababa
aba
```

출력

```
1
```

예제 설명

접기

첫 번째 예제에서 $aba$ 는 $ababa$ 의 부분 문자열로서 겹치지 않게 선택할 수 있는 최대 횟수는 $1$ 번입니다.

### 예제 2

입력

```
ababa
a
```

출력

```
3
```

예제 설명

접기

두 번째 예제에서 $a$ 는 $ababa$ 의 부분 문자열로서 겹치지 않게 최대 $3$ 번 선택할 수 있습니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!