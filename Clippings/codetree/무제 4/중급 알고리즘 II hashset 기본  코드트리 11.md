---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-elements-of-a-set/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Disjoint Set (Union Find)

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Union-Find

여러 개의 원소가 있고, 여러 개의 집합이 있다고 가정합시다. 특정 원소가 어떤 집합에 속해있는지 확인하고, 특정 집합을 합쳐야 할 일이 있다면 Union-Find 자료구조를 사용하면 좋습니다.

먼저 모든 노드가 연결되어 있지 않은 상황에서 시작합니다.  
또, **uf 배열의 초기값은 자기 자신입니다.** 이때, uf는 그룹 번호를 뜻합니다. 따라서 처음에는 모든 노드가 전부 다른 그룹에 있게 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-66737de4-9d9a-4c89-b78d-5b67cc20cfbc.png)

`union()` 연산을 사용하면, 두 노드가 같은 곳에 속해있음을 표시해줄 수 있습니다. 예를 들어 1과 3을 연결하려고 한다면, `uf[1]` 값에 3을 적어주면 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-96fbd9c1-5152-45b5-a25a-4948b72b06fc.png)

`union(5, 6)` 의 경우에도 `uf[5]` 값에 6을 적어주면 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-d92b4c71-c2ad-4e1e-b3b6-1fbb684df971.png)

이렇게 union을 이용해 두 노드를 합치게 되면 **uf 배열의 값은 그룹으로서의 의미 뿐만이 아니라, 실제 노드가 현재 가리키고 있는 부모 노드의 번호가 됩니다.**

이 상황에서 `union(5, 1)` 을 진행하면 이때는 움직임이 조금 달라집니다.

먼저, 두 노드 모두 부모 노드를 따라 올라 갈 수 있는데 까지 계속 올라가야 합니다. 이 과정을 `find()` 라고 하며, 이는 `x와 uf[x]` 값이 같아지기 전까지 계속 올라가는 것으로 구현이 가능합니다. 예를 들어 find(5)는 6이 나와야 하며, find(1)는 3이 나와야 합니다.

각 노드에 대해 find를 진행하게 되면, 두 노드 각각 루트 노드인 6, 3을 가리키게 됩니다. 이렇게 골라진 루트 노드가 X, Y였다면, `uf[X]` 에 Y를 넣어주면 됩니다. 즉, 여기서는 `uf[6]` 에 3을 넣어주게 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-955e895c-19f5-4583-8acc-ab5838b66b3f.png)

즉 union이라는 함수는 다음과 같이 적어볼 수 있습니다.

```jsx
function union(x, y)
  set X = find(x), Y = find(y)
  uf[X] = Y
```

그렇다면 find 함수는 어떻게 구현해볼 수 있을까요? x로 시작하여 계속 `uf[x]` 를 따라가다가, 더 이상 따라갈 곳이 없을 때(`uf[x] == x` 조건을 만족하는 경우)의 x 값을 반환하면 될 것입니다.

```jsx
function find(x)
  if uf[x] == x        // x가 루트 노드라면
    return x           // x 값을 반환합니다.
  return find(uf[x])   // x가 루트 노드가 아니라면, x의 부모인 uf[x]에서 더 탐색을 진행합니다.
```

즉, `find(x)` 함수는 x 노드가 포함된 집단의 루트 노드를 찾아줌과 동시에, 이 루트 노드가 그 집단을 대표하는 대표 번호가 됩니다. 다음 그림에서 1, 3, 5, 6번 노드는 모두 대표 번호가 3번이 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-955e895c-19f5-4583-8acc-ab5838b66b3f.png)

여기에 `union(4, 1)` 를 한번 진행하게 되면, 4의 루트 노드는 4, 1의 루트 노드는 3 이므로 다음과 같이 그림이 바뀌게 됩니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-7321a5f1-dad1-4818-b9a7-6571c8c98f78.png)

이러한 Union-Find는 꽤나 쓸만한 자료구조이지만, 약간 문제가 있습니다.

다음과 같이 모든 집합들이 합쳐있다고 가정합시다.

![](https://contents.codetree.ai/problems/1889/images/introductions-d4fcfe37-69fa-44a1-9206-8adc92c73234.png)

이런 경우, 9번에 대해 find를 호출하면 조상을 찾을 때 까지 계속 앞으로 나아가야 하고, 결국 $O(N)$ 이라는 시간이 소요됩니다. 사실 이렇게 되면 굳이 자료구조를 만들면서까지 사용할 이유가 없어지죠. 왜냐하면 일반 배열을 만들어서 $O(N)$ 에 각 노드가 어디에 해당하는지를 표기해주는 식으로도 충분히 union, find 함수를 흉내낼 수 있기 때문입니다.

그래서 개선책이 등장하였습니다. find를 호출할때 조상을 찾아내면, 현재 값의 부모값을 조상으로 바꿔버리는 것입니다.

현재 집합 구조가 다음과 같다고 가정해 봅시다.

![](https://contents.codetree.ai/problems/1889/images/introductions-a3099e46-5a7f-4d8d-a4de-9aa04d766e1d.png)

여기서 `find(5)` 가 수행되었을 때, 5 위에 있는 모든 노드들을 전부 루트 노드인 3으로 옮겨버리겠다는 뜻입니다. 마치 다음과 같이요.

![](https://contents.codetree.ai/problems/1889/images/introductions-ff0972ed-0d06-447b-9bf4-3dda4a7b1fe0.png)

맨 앞에서 봤던 다음 예시에서, find(9)가 실행된다면 결과가 어떻게 바뀐다는 것일까요?

![](https://contents.codetree.ai/problems/1889/images/introductions-d4fcfe37-69fa-44a1-9206-8adc92c73234.png)

바로 다음과 같이 9 위에 있는 모든 노드들이 전부 노드 1을 가리키게 한다는 것입니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-7e38aed9-267f-4305-a26c-64ff839af5fb.png)

이것이 만약 가능하다면, find 함수가 호출될 때마다 탐색했던 모든 노드가 전부 root로 붙게 되 깊이가 전부 1로 바뀌게 되므로, 이후 동일한 노드를 탐색하게 될 경우 시간이 거의 소요되지 않게 됩니다. 즉, 중복 탐색하는 경우가 많이 사라지게 됩니다. 이러한 방법을 **경로 압축(Path Compression)** 이라고 부르며, 이 방법을 union-find에 적용하면, union, find 함수의 시간복잡도가 모두 $O(log N)$ 이 됩니다.

이 경로 압축 기법에 대한 구현은, 기존 find 함수에 몇 줄만 수정해주면 됩니다.

기존 find 함수는 다음과 같았습니다.

```jsx
function find(x)
  if uf[x] == x        // x가 루트 노드라면
    return x           // x 값을 반환합니다.
  return find(uf[x])   // x가 루트 노드가 아니라면, x의 부모인 uf[x]에서 더 탐색을 진행합니다.
```

여기서 `find(uf[x])` 부분만 다음과 같이 수정하면 됩니다.

```jsx
function find(x)
  if uf[x] == x                 // x가 루트 노드라면
    return x                    // x 값을 반환합니다.
  set root_node = find(uf[x])   // x가 루트 노드가 아니라면, x의 부모인 uf[x]에서 더 탐색을 진행합니다.
  uf[x] = root_node             // 노드 x에 부모를 루트 노드로 설정해줍니다.
  return root_node              // 찾아낸 루트 노드를 반환합니다.
```

기존에는 루트 노드를 찾아 바로 반환해줬었는데, 이제는 반환 전에 거쳐가게 되는 모든 노드 x에 대해 `uf[x]` 값을 루트 노드로 바꿔준 뒤, 루트 노드를 반환해주면 됩니다.

이를 노드가 9개였던 경우를 예시로 `find(9)` 함수 호출시의 결과를 시각적으로 살펴보면 다음과 같습니다.

![](https://contents.codetree.ai/problems/1889/images/introductions-6a392668-3222-4b00-ae6c-61282187a4ff.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-adb99d5b-e8fc-4a25-8b4e-e53abc2badac.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-74d98ef1-041a-4740-813b-71b3a556a47f.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-59caf64a-2d71-4d41-8723-fcbe67be08b6.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-ff7a802e-b9fa-49a9-bc13-d954d1664b80.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-46728bff-2a2b-4229-98e7-c4ecda8bcd38.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-49208c29-2d91-40d2-b728-46ca62668fec.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-1a3986a2-ce9b-47ad-bc70-207004170bed.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-6f2c11a4-1b0f-4ba1-881d-5780e73c0ff8.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-8ea40a6f-a9a9-42e6-b1ce-c15f87856c8f.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-3bd9b747-2386-40c9-a076-40bb8c47b9fb.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-5a0310bb-bc4a-4561-b972-3ec71aee3dcb.png) ![](https://contents.codetree.ai/problems/1889/images/introductions-523fe3a9-cb38-44be-8d95-f668be08f906.png)

1 / 13

이런식으로 개선을 하게 되면 이전 알고리즘에 비해 훨씬 개선되는 것을 볼 수 있습니다!

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.