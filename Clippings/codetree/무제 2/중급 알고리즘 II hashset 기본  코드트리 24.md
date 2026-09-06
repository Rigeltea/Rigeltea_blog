---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-circle-dance/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 6. Doubly-LinkedList

## 강강수월래

Hard

90XP

평균 180분

43% 정답률

총 제출 219회

현재 코드트리 고등학교의 수련회에서는 마지막 날 밤 행사로 학생들이 원 모양으로 손을 잡고 빙빙 도는 강강수월래를 진행하고 있습니다. 수련회의 총 교관인 곰돌이는 학생들에게 다음과 같은 $3$ 가지 동작을 실시하도록 하였습니다.

1. $A$ 학생과 $B$ 학생이 있는 원 잇기
2. 한 원 안에 있는 학생 $A$, $B$ 각각을 경계로 원 쪼개기 ($A$ 학생부터 시작해 시계 방향으로 돌면서 $B$ 학생을 만날 때까지의 학생들을 새로운 원으로 만들어 원래 원에서 쪼개집니다.)
3. $A$ 학생이 속한 원 안에서 학생 번호가 가장 작은 학생부터 반시계 방향으로 자신의 번호 외치기

$1$ 번 행동의 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/4010/images/problems-41328eac-f598-4465-aee9-3ec052a7cba5.png)

다음과 같은 두 원을 합친다고 해보겠습니다.

![](https://contents.codetree.ai/problems/4010/images/problems-f3356bc6-641a-44bd-bad2-3adc55724f66.png)

다음과 같이 원을 잇습니다. 잇고 나면 다음과 같이 변화합니다.

![](https://contents.codetree.ai/problems/4010/images/problems-dc9af0e9-7f51-4148-83a8-fd066de968aa.png)

$2$ 번 행동의 예시는 다음과 같습니다.

![](https://contents.codetree.ai/problems/4010/images/problems-0a58d7ac-9191-4b68-ab16-125f7338ae0c.png)

다음과 같은 상황에서 원을 나눈다고 해보겠습니다.

![](https://contents.codetree.ai/problems/4010/images/problems-5585a98d-db37-43f1-af46-718c0f8be0b6.png)

다음과 같이 원이 나뉘게 됩니다.

다음 행동을 진행할 수 있는 프로그램을 작성하세요.

### 입력

첫 번째 줄에 학생의 수 $N$ 과 제일 처음에 있는 원의 수 $M$, 동작의 총 횟수 $Q$ 가 공백을 사이에 두고 주어집니다.

두 번째 줄부터 $M$ 개의 줄에 걸쳐 각 원에 있는 학생들에 대한 정보가 주어집니다. 각 줄에 맨 첫 수로는 각 원에 있는 학생의 총 수가 주어집니다. 그 뒤부터 공백을 사이에 두고 학생들의 번호가 시계 방향으로 순서대로 공백을 사이에 두고 주어집니다.

$M + 2$ 번째 줄부터 $Q$ 개의 줄에 걸쳐 곰돌이가 지시한 동작이 다음과 같은 형식으로 주어집니다.

### 제한 조건

- $2 \le N \le 100\,000$
- $2 \le M \le 10$
- $1 \le Q \le 10\,000$
- $1 \le \texttt{학생의 번호} \le 100\,000\,000$
- 학생의 번호는 모두 다르다고 가정해도 좋습니다.

### 출력

$3$ 번 명령은 맨 마지막에만 주어집니다. $3$ 번 명령이 주어졌을 때 $A$ 학생이 속한 원 안에서 학생 번호가 가장 작은 학생부터 반시계 방향으로 돌면서 해당 원의 모든 학생들의 번호를 공백을 사이에 두고 출력하세요.

### 입력 예제

### 예제 1

입력

```
8 2 3
3 1 4 3
5 2 8 7 5 6
1 4 6
2 6 7
3 4
```

출력

```
1 3 5 7 4
```

### 제한

• Time Limit: 1000 ms

• Memory Limit: 100 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!