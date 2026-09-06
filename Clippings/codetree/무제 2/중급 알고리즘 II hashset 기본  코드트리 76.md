---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/test-longest-student/description"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Dijkstra

## 가장 오래 걸리는 학생

Easy

20XP

평균 15분

72% 정답률

총 제출 277회

$N$ 개의 서로 다른 장소가 있습니다. $1$ 번부터 $N-1$ 번 장소에는 학생이 한 명씩 살고 있고, $N$ 번 장소는 학교입니다. 두 개의 장소를 연결하는 간선은 없거나, 있다면 최대 $1$ 개만 있으며 주어지는 모든 간선은 방향성을 갖지 않습니다. 간선마다 길이가 주어지며, 각 학생은 등교 시 최단거리로 학교로 이동한다고 합니다. 모든 학생은 거리 $1$ 을 이동하는 데 $1$ 초의 시간이 걸린다고 했을 때, 학교에 등교하는 데 가장 오래 걸리는 학생의 소요 시간을 구하는 프로그램을 작성해보세요.

### 입력

첫 번째 줄에는 $N$ (장소의 개수)과 $M$ (간선의 개수)이 공백을 사이에 두고 차례대로 주어집니다.

두 번째 줄에는 간선을 이루고 있는 두 장소의 번호 $i$, $j$ 와 간선의 길이 $d$ 가 각각 공백을 사이에 두고 차례대로 주어집니다.

### 제한 조건

- $1\le N\le 100\,000$
- $1\le M\le 100\,000$
- $1\le d\le 1\,000$
- 모든 학생이 등교하는 것이 가능함을 가정해도 좋습니다.

### 출력

첫 번째 줄에 가장 등교하는 데 오래 걸리는 학생의 소요 시간을 출력합니다.

### 입력 예제

### 예제 1

입력

```
5 6
1 2 1
5 1 2
5 4 100
4 3 5
2 4 9
2 3 3
```

출력

```
11
```

예제 설명

접기

![](https://contents.codetree.ai/problems/2234/images/problems-571ef182-c066-43ff-87eb-75d60e0273b2.png)

$1$ 번 장소에서 시작하여 학교로 이동할 때 필요한 간선 한 개입니다. 따라서 간선 길이의 합은 $2$ 입니다.

![](https://contents.codetree.ai/problems/2234/images/problems-848c21aa-cb86-4e7e-9c1e-8b8c9967966b.png)

$2$ 번 장소에서 시작하여 학교로 이동할 때 거쳐야 하는 간선 길이의 합은 $1+2=3$ 입니다.

![](https://contents.codetree.ai/problems/2234/images/problems-5df6cd37-64df-42b9-af78-589faefaf34d.png)

$3$ 번 장소에서 시작하여 학교로 이동할 때 거쳐야 하는 간선 길이의 합은 $3+1+2=6$ 입니다.

![](https://contents.codetree.ai/problems/2234/images/problems-e630f981-5a53-4025-99d0-0672abdc6bd1.png)

$4$ 번 장소에서 시작하여 학교로 이동할 때 거쳐야 하는 간선 길이의 합은 $5+3+1+2=11$ 입니다.

![](https://contents.codetree.ai/problems/2234/images/problems-a801a26f-1040-46ce-a164-d3f8bef4a60b.png)

즉, $4$ 번 장소에 있는 학생이 $5$ 번 장소에 가기 위한 최단 거리는 $11$ 입니다. 이보다 더 오래 걸리는 학생은 없습니다.

### 제한

• Time Limit: 2000 ms

• Memory Limit: 80 MiB

이 콘텐츠가 도움이 되었나요?

개념이 아직 헷갈리신다면 한 번 더 확인해보세요!