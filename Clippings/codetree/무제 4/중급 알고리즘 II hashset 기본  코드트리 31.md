---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-find-the-location-of-a-substring/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. String Hashing

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## String Hashing

Python에서는 set, dict라는 class가 있습니다. set과 dict는 각각 HashSet, HashMap 자료구조로 되어있으며, 이 HashSet과 HashMap은 [해싱](https://www.codetree.ai/missions/6/problems/hash-introduction/introduction) 을 기반으로 데이터들을 관리해주는 자료구조 입니다. 따라서 삽입, 삭제, 탐색 등 모든 함수의 시간복잡도가 전부 $O(1)$ 입니다.

이때 key로 문자열(string)이 주어진 경우에도 해싱이 제대로 동작하기 위해서는 적절한 대표값을 찾아주는 과정이 필요합니다. 이러한 과정을 String Hashing이라 부르며, 만약 이러한 과정이 없다면 일치하는 문자열이 존재하는지를 판단하기 위해 모든 문자열에 대해 각각의 길이만큼 순회하며 일치하는 문자열이 있는지를 확인해야만 할 것입니다.

String Hashing 방법 중 많이 사용되는 해싱 방법으로는 Polynomial Rolling Hash가 있습니다. Polynomial Rolling Hash는 아래와 같이 진법의 형태처럼 hashing을 진행하는 것을 의미합니다.

$$
hash(s) = s[0] * p^{n-1} +s[1]*p^{n-2}+s[2]*p^{n-3}+....+s[n-2]*p+s[n-1] \mod m
$$

만약 문자열 s가 "1938274"와 같이 수들로만 이루어져 있다면 각 자리에는 '0'부터 '9'까지의 문자만 올 수 있습니다. 이를 진법으로 표현하기 위해서는 p가 10 이상이어야 하고, 그래야 서로 다른 문자열에 대해 서로 다른 hash 값을 갖게 될 것입니다. **보통 p는 표현해야 하는 서로 다른 문자의 수보다 조금 큰 소수로 정합니다.** 따라서 문자열이 전부 숫자로만 이루어져 있다면 p를 11로 잡는 것이 적합합니다. 만약 알파벳 소문자로만 이루어진 문자열이라면 소문자 알파벳은 26개가 있으므로 p를 31로, 대소문자 알파벳으로만 이루어져 있는 경우에는 53으로 잡고는 합니다. 이때 'a', 'b', 'c',..는 순서대로 1부터 26까지 대응시킵니다. 0부터 시작하지 않는 이유는 그러했을 때 a, aa, aaa,.. 은 서로 다른 문자열이지만 해싱 값이 전부 0이 되어버리기 때문에 이를 방지하는것이 좋습니다.

이렇게 단순히 p진법의 형태로 hash값을 나타낼 수 있다면 좋겠지만, 실제 이 값은 굉장히 커질 수 있기 때문에 계산하는데 속도도 오래 걸리고 C++/Java 등의 언어에서는 값을 표현하기가 힘들 수도 있습니다. 따라서 m으로 나눈 나머지를 hash값으로 계산하며, 이때 m이 클수록 해싱에서 충돌이 일어날 확률이 줄어들기에 m은 아주 큰 소수인 10억 7이나 10억 9 정도로 잡고는 합니다.

예로 아래는 `banana` 라는 문자열의 해싱값을 구하는 코드입니다. 시간복잡도는 $O(N)$ 이 됩니다.

```python
s = "banana"
n = len(s)

# p, m을 설정합니다.
p = 31
m = int(1e9) + 7

# p_pow 값을 계산합니다.
# p_pow[i] = p^i % m
p_pow = [0] * (n + 1)
p_pow[0] = 1
for i in range(1, n + 1):
    p_pow[i] = (p_pow[i - 1] * p) % m

# 해싱값을 계산합니다.
# h = (s[0] * p^(n - 1) + s[1] * p^(n - 2) + ... + s[n - 1] * 1) % m
h = 0
for i in range(n):
    int_s = ord(s[i]) - ord('a') + 1
    h = (h + int_s * p_pow[n - 1 - i]) % m

# 해싱 결과
print(h)
```

## Rabin Karp 알고리즘

두 문자열 T, P가 주어졌을 때 문자열 T의 부분 문자열 중 문자열 P와 일치하는 경우가 있는지를 판단해보려고 합니다. 문자열 T의 길이를 n, 문자열 P의 길이를 l이라 했을 때 완전탐색을 이용하면 문자열 T에서 매칭이 시작될 위치를 선정한 뒤 l개의 문자를 비교해보는 식으로 $O(NL)$ 에 구현이 가능합니다.

```python
T = "banana"
P = "nan"
n = len(T)
l = len(P)

exists = False
for i in range(n - l + 1):
    if T[i:i+l] == P:
        exists = True

print(exists)
```

이를 Polynomial Rolling Hash을 통해 $O(N + L)$ 로 줄일 수 있으며 이를 **Rabin Karp** 알고리즘이라 부릅니다.

만약 위에 코드에서 두 문자열이 일치하는지를 판단하는 부분이 **두 해싱값이 일치하는지** 로 바뀐다면 시간을 줄일 수 있다는 점을 이용한 것입니다.

P의 길이는 l로 고정되어 있기에 $O(L)$ 에 해싱값을 구해주면 됩니다.  
T의 경우 길이가 l인 부분 문자열을 순서대로 잡아보며 각각의 해싱값을 구해내는 것이 중요합니다. 이는 처음 \[0, l - 1\] 구간에 해당하는 해싱 값, \[1, l\] 구간에 해당하는 해싱 값,..., \[n - l, n - 1\] 구간에 해당하는 해싱값을 전부 구해야 하는 것입니다. 이걸 기존 해싱 값을 계산하듯 똑같이 계산한다면 시간복잡도는 여전히 $O(NL)$ 이 될 것입니다.

![](https://contents.codetree.ai/problems/3413/images/introductions-1d9206c1-0db5-4c79-a1ca-163036a8c223.png)

이때 중요한 관찰 중 하나는 **인접한 구간으로 넘어갈 때 바뀌는 값이 양 옆 경계 2개 밖에 없다는 것입니다.** 위의 예에서 처음 "ban"에서 그 다음 "ana"로 넘어가게 될 때를 생각해보면 맨 앞에 있던 b가 빠지고, 맨 뒤에 a가 새롭게 추가되는 일만 일어난다는 것입니다. 즉, 이미 계산된 기존 해싱값을 이용해서 $O(1)$ 에 그 다음 해싱값을 계산할 수 있게 됩니다.

현재 계산하려고 하는 구간이 \[i, i + l - 1\]라고 해보겠습니다. 그러면 이미 계산된 값 $h_{i-1}$ 은 \[i - 1, i + l - 2\]에 해당하는 해싱값일 것입니다. 각 해싱값은 아래와 같이 계산됩니다.

$$
hash(T[i - 1, i + l - 2]) = T[i - 1] * p^{l-1} +T[i]*p^{l-2}+....+T[i+l-3]*p+T[i+l-2] \mod m.
$$
 
$$
hash(T[i, i + l - 1]) = T[i] * p^{l-1} +T[i+1]*p^{l-2}+....+T[i+l-2]*p+T[i+l-1] \mod m.
$$

위에 식에 p를 곱하면 아래 식이 나오게 되고

$$
p \times hash(T[i - 1, i + l - 2]) = T[i - 1] * p^l +T[i]*p^{l-1}+....+T[i+l-3]*p^2+T[i+l-2]*p \mod m.
$$

여기에서 $T[i - 1] * p^l$ 를 빼고 새롭게 $T[i+l-1]$ 을 더해주게 되면 식이 $hash(T[i, i + l - 1])$ 와 같아짐을 확인할 수 있습니다.

$$
\begin{aligned}
p \times hash(T[i - 1, i + l - 2]) - T[i - 1] * p^l + T[i+l-1] = \\ T[i - 1] * p^{l-1} +T[i]*p^{l-2}+....+T[i+l-3]*p+T[i+l-2] \mod m
\end{aligned}
$$

따라서 그 다음 해싱값인 $h_i$ 는 $p \times h_{i-1} - T[i - 1] * p^l + T[i+l-1]$ 로 $O(1)$ 에 바로 계산이 가능합니다. 이제 각 해싱값이 일치하는 경우가 있는지를 확인하면 되므로 $O(N + L)$ 에 부분문자열 여부를 판단할 수 있습니다.

```python
T = "banana"
P = "nan"
n = len(T)
l = len(P)

# p, m을 설정합니다.
p = 31
m = int(1e9) + 7

# p^i, 값을 m으로 나눈 나머지를 관리합니다.
p_pow = [0] * (n + 1)

# 소문자 알파벳을 수로 변경합니다.
def to_int(c):
    return ord(c) - ord('a') + 1

# p_pow 값을 계산합니다.
# p_pow[i] = p^i % m
p_pow[0] = 1
for i in range(1, n + 1):
    p_pow[i] = (p_pow[i - 1] * p) % m

# pattern에 대한 해싱값인 p_h값을 계산합니다.
# p_h = (P[0] * p^(l - 1) + P[1] * p^(l - 2) + ... + P[l - 1] * 1) % m
# 소문자 알파벳은 a부터 z까지 순서대로 1부터 26까지의 수와 대응됩니다.
p_h = 0
for i in range(l):
    p_h = (p_h + to_int(P[i]) * p_pow[l - 1 - i]) % m

# text에서 구간 [0, l - 1]에 해당하는 해싱값을 계산합니다.
t_h = 0
for i in range(l):
    t_h = (t_h + to_int(T[i]) * p_pow[l - 1 - i]) % m

exists = False
# 이미 일치한다면 존재하는 것입니다.
if p_h == t_h:
    exists = True

# text에서
# 길이가 l인 부분문자열을 전부 잡아봅니다.
for i in range(1, n - l + 1):
    # 이전 [i - 1, i + l - 2]에 해당하는 해싱값은 t_h에 있습니다.
    # 이전 값(t_h)은 (T[i - 1] * p^(l - 1) + T[i] * p^(l - 2) + ... + T[i + l - 2] * 1) % m입니다.
    # 이제 t_h * p - T[i - 1] * p^l + T[i + l - 1]를 계산하면
    # 새로 계산을 원하는 해싱값인 (T[i] * p^(l - 1) + T[i + 1] * p(l - 2) + ... + T[i + l - 1] * 1) % m이 됩니다.
    t_h = (t_h * p - to_int(T[i - 1]) * p_pow[l] + to_int(T[i + l - 1])) % m
    # t_h값을 양수로 변환해줍니다.
    if t_h < 0:
        t_h += m

    # 값이 일치한다면 존재하는 것입니다.
    if p_h == t_h:
        exists = True

print(exists)
```

## Collision 예방

m이 10억은 $10^9$ 으로 큰 값이기에 충돌이 발생할 확률은 $\frac{1}{m}$ 이 됩니다. 하지만 이것은 한 번의 충돌에 대한 얘기일 뿐, 만약 $10^6$ 개의 서로 다른 문자열이 주어져 있다면 충돌이 일어날 확률은 $10^{-3}$ 으로 굉장히 높아지게 됩니다. 만약 서로 다른 문자열의 수를 세어야 하는 상황이라면 모든 문자열간의 충돌을 고려해야 하기에 이는 1에 가까운 확률로 충돌이 발생하게 됩니다. 이러한 경우에는 hashing을 2개 이상 적용하여 각각의 해싱 값이 전부 일치하는지를 확인하는 방법을 이용하여 쉽게 해결할 수 있습니다. 예로 첫 번째 해싱으로는 p=31, m=10억 7을, 두 번째 해싱으로는 p=37, m=10억 9 조합을 사용하면 두 값이 모두 일치하는 경우에만 충돌이 일어나게 되는데, 이때의 단일 충돌이 일어날 확률은 실제 두 m이 곱해진 값($10^{18}$)으로 해싱을 했을 때와 비슷해지기 때문에 이 경우에는 모든 문자열 쌍에 대한 비교를 하더라도 충돌이 일어날 확률이 $10^{-6}$ 정도로 굉장히 작아지게 됩니다. 이처럼 문자열 비교 횟수가 많은 경우라면 꼭 2개 이상의 해싱을 사용하여 충돌이 일어나지 않도록 해야 함에 유의합니다.

**따라서 문제풀이에 있어서는 항상 안정적으로 최소 2개의 해싱을 사용하는 것을 권장드립니다.**

예를 들어 Rabin Karp 알고리즘의 경우 아래와 같이 2개의 (p, m) 조합을 이용해 구현할 수 있습니다.

```python
T = "banana"
P = "nan"
n = len(T)
l = len(P)

# 2개의 polynomial rolling 해싱을 위한 p, m 값을 정의합니다.
p = [31, 37]
m = [int(1e9) + 7, int(1e9) + 9]

# p^i, 값을 m으로 나눈 나머지를 관리합니다.
p_pow = [
    [0] * (n + 1)
    for _ in range(2)
]

# 소문자 알파벳을 수로 변경합니다.
def to_int(c):
    return ord(c) - ord('a') + 1

# p_pow 값을 계산합니다.
# p_pow[i] = p^i % m
for k in range(2):
    # p_pow[i] = p^i % m
    p_pow[k][0] = 1
    for i in range(1, n + 1):
        p_pow[k][i] = (p_pow[k][i - 1] * p[k]) % m[k]

# pattern에 대한 해싱값인 p_h값을 계산합니다.
# p_h = (P[0] * p^(l - 1) + P[1] * p^(l - 2) + ... + P[l - 1] * 1) % m
# 소문자 알파벳은 a부터 z까지 순서대로 1부터 26까지의 수와 대응됩니다.
p_h = [0, 0]
for k in range(2):
    for i in range(l):
        p_h[k] = (p_h[k] + to_int(P[i]) * p_pow[k][l - 1 - i]) % m[k]

# text에서 구간 [0, l - 1]에 해당하는 해싱값을 계산합니다.
t_h = [0, 0]
for k in range(2):
    for i in range(l):
        t_h[k] = (t_h[k] + to_int(T[i]) * p_pow[k][l - 1 - i]) % m[k]

exists = False
# 이미 일치한다면 존재하는 것입니다.
if p_h[0] == t_h[0] and p_h[1] == t_h[1]:
    exists = True

# text에서
# 길이가 l인 부분문자열을 전부 잡아봅니다.
for i in range(1, n - l + 1):
    for k in range(2):
        # 이전 [i - 1, i + l - 2]에 해당하는 해싱값은 t_h에 있습니다.
        # 이전 값(t_h)은 (T[i - 1] * p^(l - 1) + T[i] * p^(l - 2) + ... + T[i + l - 2] * 1) % m입니다.
        # 이제 t_h * p - T[i - 1] * p^l + T[i + l - 1]를 계산하면
        # 새로 계산을 원하는 해싱값인 (T[i] * p^(l - 1) + T[i + 1] * p(l - 2) + ... + T[i + l - 1] * 1) % m이 됩니다.
        t_h[k] = (t_h[k] * p[k] - to_int(T[i - 1]) * p_pow[k][l] + to_int(T[i + l - 1])) % m[k]
        # t_h값을 양수로 변환해줍니다.
        if t_h[k] < 0:
            t_h[k] += m[k]

    # 값이 일치한다면 존재하는 것입니다.
    if p_h[0] == t_h[0] and p_h[1] == t_h[1]:
        exists = True

print(exists)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.