---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-longest-palindrome-3/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Manacher's algorithm

## 가장 긴 좌우 대칭인 문자열 찾기 3

Medium

60XP

평균 26분

54% 정답률

총 제출 92회

길이가 $n$ 인 문자열 $S$ 와 소문자 알파벳 $c$ 가 주어졌을 때 해당 문자열에 포함된 연속한 문자열 중 가장 긴 좌우대칭인 문자열을 구하는 프로그램을 작성해보세요. 단, 소문자 알파벳 $c$ 를 포함하지 않는 부분 문자열 중 가장 긴 좌우대칭인 문자열을 구해야만 함에 유의합니다.

### 입력

첫 번째 줄에는 문자열 $S$ 의 길이를 나타내는 $n$ 과 포함해서는 안되는 소문자 알파벳 $c$ 가 공백을 사이에 두고 주어집니다.  
두 번째 줄에는 문자열 $S$ 가 주어집니다. 문자열 $S$ 는 소문자 알파벳으로만 이루어져 있습니다.

### 제한 조건

- $1 \le n \le 300,000$

### 출력

소문자 알파벳 $c$ 를 포함하지 않는 부분문자열 중 가장 긴 좌우대칭인 문자열의 길이를 출력합니다. 그러한 문자열이 없다면 $0$ 을 출력합니다.

### 입력 예제

### 예제 1

입력

```
6 c
baabcb
```

출력

```
4
```

### 예제 2

입력

```
6 a
baabcb
```

출력

```
3
```

### 제한

• Time Limit: 5000 ms

• Memory Limit: 288 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!