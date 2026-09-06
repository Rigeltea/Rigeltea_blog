---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-invitation-and-number-tag/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. HashSet

## 초대장과 번호표

Hard

70XP

평균 180분

42% 정답률

총 제출 1,311회

$1$ 번 부터 $N$ 번까지 번호표를 가진 총 $N$ 명의 사람들이 있습니다.  
여기에 총 $G$ 개의 그룹이 있습니다. 그룹은 아래의 조건을 만족합니다.

- 같은 사람이 동시에 여러 그룹에 속할 수 있습니다.
- 그룹 내 모든 멤버가 정확히 일치하는 두 그룹은 없습니다.

사람들에게 초대장을 나눠주려 하는데, 그룹 인원수가 $k$ 인 그룹에서 $k-1$ 명의 사람들이 초대장을 받았다면 나머지 한 사람도 무조건 초대장을 받아야합니다. $1$ 번 사람에게는 무조건 초대장을 준다고 할 때, 확실하게 초대장을 받게 되는 인원 수를 구하는 프로그램을 작성하세요.

### 입력

첫 번째 줄에는 $N$, $G$ 가 공백을 사이에 두고 차례대로 주어집니다.

두 번째 줄 부터는 $G$ 개의 줄에 걸쳐 각 줄에 각 그룹의 인원수와 해당 그룹에 속하는 사람의 번호가 공백을 사이에 두고 차례대로 주어집니다.

### 제한 조건

- $1 \le \texttt{그룹 내 인원수} \le N$
- $1 \le N \le 100\,000$
- $2 \le G \le 250\,000$
- $\texttt{모든 그룹 내 사람 수의 총합} \le 250\,000$

### 출력

첫 번째 줄에 확실하게 초대장을 받게 되는 인원 수를 출력합니다.

### 입력 예제

### 예제 1

입력

```
10 4
2 1 3
2 3 4
6 1 2 3 4 6 7
4 4 3 2 1
```

출력

```
4
```

예제 설명

접기

그룹 $1$ 에서 $1$ 번 사람을 초대했기 때문에 $3$ 번 사람을 무조건 초대해야합니다. 그룹 $2$ 에서 $3$ 번 사람을 초대했기 때문에 무조건 $4$ 번 사람을 초대해야합니다. 그룹 $4$ 에서 $1$, $3$, $4$ 번 사람을 초대했기 때문에 무조건 $2$ 번 사람을 초대해야 합니다. 따라서 총 $4$ 명의 사람은 꼭 초대를 받게 됩니다.

### 제한

• Time Limit: 1000 ms

• Memory Limit: 100 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!