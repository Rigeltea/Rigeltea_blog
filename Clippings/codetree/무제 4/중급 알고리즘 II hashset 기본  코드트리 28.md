---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-longest-palindrome-2/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 1. Manacher's algorithm

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Manacher's Algorithm

abaccaba와 같이 뒤집었을 때의 결과가 동일할 때 이러한 문자열을 팰린드롬(palindrome)이라고 합니다. 문자열이 하나 주어졌을 때 해당 문자열의 부분 문자열(포함된 연속한 문자열) 중 가장 긴 팰린드롬의 길이를 구해보려고 합니다. 예를 들어 bananac의 부분 문자열 중 가장 긴 팰린드롬은 anana로 길이는 5가 됩니다.

이 문제를 가장 간단히 해결해볼 수 있는 방법은 문자열을 순회하며 가능한 모든 경우에 대하여 탐색하는 완전탐색을 진행하는 것입니다. 문자열을 앞에서부터 순회하면서 시작점 후보를 정하고, 나머지 모든 문자 각각을 끝 점 후보로 설정했을 때 좌우대칭인지 여부를 판별하여 길이가 가장 긴 후보를 구하는 방법입니다. 이 방법의 시간복잡도는 $O(N^3)$ 이 됩니다.

```python
input_str = "bananac"
ans = 0

# 주어진 문자열이
# palindrome인지 판별합니다.
def is_palindrome(string):
    # 하나라도 일치하지 않으면 palindrome이 아닙니다.
    n = len(string)
    for i in range(n):
        if string[i] != string[n - i - 1]:
            return False

    return True

   
# 문자열을 앞에서부터 순회하며 시작점 후보를 정합니다.
for start in range(len(input_str)):
    # 시작점을 포함한 나머지 문자열을 순회하며 끝점 후보를 정합니다.
    for end in range(start, len(input_str)):
        candidate = input_str[start:end + 1]
        # 문자열이 좌우로 대칭이고 지금까지 저장된 정답보다 긴 경우 답을 갱신합니다.
        if is_palindrome(candidate):
            ans = max(ans, len(candidate))

print(ans)
```

관점을 바꿔 각 문자에 대해 좌우대칭인 문자열의 중심일 때를 가정하여 확장해나가는 완전탐색을 진행해볼 수 있습니다. 문자열을 앞에서부터 순회하면서 각 문자를 중심점이라 가정했을 때 최대 확장 가능한 좌우대칭인 문자열을 구하는 방법입니다. 이 때, 좌우대칭인 문자열은 “aba”와 같은 홀수이거나 “abba”와 같은 짝수일 수 있습니다. 따라서 각각의 경우에 대하여 모두 구해준 뒤 최대인 문자열을 구해줍니다.

이렇게 중심점을 가정하면 팰린드롬의 특성상 최대 확장 가능한 좌우대칭인 문자열을 $O(N)$ 에 찾을 수 있게 됩니다. 따라서 중심점 설정에 $O(N)$ \* 확장 가능한 범위를 탐색하는 데 $O(N)$ 의 시간이 소요되므로 총 시간복잡도는 $O(N^2)$ 이 됩니다.

```python
input_str = "bananac"
ans = 0

def get_max_palindrome_length(start, end):
    # 문자열 범위를 벗어나지 않으면서 좌우가 대칭인 경우 확장해나갑니다.
    while start >= 0 and end < len(input_str) and \
          input_str[start] == input_str[end]:
        start -= 1
        end += 1

    # while문이 끝났을 때 start와 end는 각각 좌우가 대칭이 깨진 첫 문자의 인덱스를
    # 가리키고 있기 때문에 이를 보정해줍니다.
    start += 1
    end -= 1

    return end - start + 1

   
# 문자열을 앞에서부터 순회하며 중간점 후보를 정합니다 (중심 길이는 1).
for center in range(len(input_str)):
    # 최장 팰린드롬의 길이를 구해 답을 갱신합니다.
    ans = max(ans, get_max_palindrome_length(center, center))

# 문자열을 앞에서부터 순회하며 중간점 후보를 정합니다 (중심 길이는 1).
for center in range(len(input_str) - 1):
    # 최장 팰린드롬의 길이를 구해 답을 갱신합니다.
    ans = max(ans, get_max_palindrome_length(center, center + 1))

print(ans)
```

이때 홀수 길이의 팰린드롬, 짝수 길이의 팰린드롬을 굳이 구분하지 않고 코드를 작성할 수 있는 방법이 있습니다. 바로 주어진 문자열 내 문자 사이사이에 # 문자를 추가해준 뒤 (양쪽 경계 포함) 가장 긴 홀수 팰린드롬의 길이를 구해주는 것입니다.

예로 bananac가 주어진 경우 이를 #b#a#n#a#n#a#n#로 변경한 뒤 가장 긴 홀수 팰린드롬을 구하면 #a#n#a#n#a#이 됩니다. 이렇게 #을 추가하게 되면 항상 홀수 길이의 팰린드롬만 고려해서 답을 구하면 되고, 실제 문자열에서의 팰린드롬의 길이는 이렇게 구해진 길이를 2로 나눈 몫이 됩니다. 여기서는 #a#n#a#n#a#의 길이인 11을 2로 나눈 몫인 5가 답이 되는 것입니다.

```python
input_str = "bananac"
ans = 0

# 주어진 문자열 내 문자 사이사이에 #을 넣어줍니다. (양쪽 경계 포함)
input_str = "#" + "#".join(input_str) + "#"

def get_max_palindrome_length(start, end):
    # 문자열 범위를 벗어나지 않으면서 좌우가 대칭인 경우 확장해나갑니다.
    while start >= 0 and end < len(input_str) and \
          input_str[start] == input_str[end]:
        start -= 1
        end += 1

    # while문이 끝났을 때 start와 end는 각각 좌우가 대칭이 깨진 첫 문자의 인덱스를
    # 가리키고 있기 때문에 이를 보정해줍니다.
    start += 1
    end -= 1

    return end - start + 1

   
# 문자열을 앞에서부터 순회하며 중간점 후보를 정합니다 (중심 길이는 1).
for center in range(len(input_str)):
    # 최장 팰린드롬의 길이를 구해 답을 갱신합니다.
    ans = max(ans, get_max_palindrome_length(center, center))

# 처음 주어진 문자열에서 
# #을 제외한 부분의 길이가 실제 답이 되기에
# 2로 나눴을 때의 몫이 답이 됩니다.
print(ans // 2)
```

**Manacher's algorithm을 이용하면 최장 홀수 팰린드롬의 길이를 $O(N)$ 에 구할 수 있습니다.** 위에서 일반적으로 최장 팰린드롬의 길이는 #을 문자 사이사이에 붙여 홀수 팰린드롬을 구하는 방법으로 계산할 수 있다고 했기에, 최장 홀수 팰린드롬의 길이만 빠르게 구할 수 있으면 충분합니다.

Manacher's algorithm은 먼저 A라는 배열을 정의하는 것에서 시작합니다. $A_i$ 는 i 번지를 중심으로 하는 홀수 길이의 팰린드롬 중 가장 긴 팰린드롬의 반지름의 길이를 뜻합니다. 즉, $[i - A_i, i + A_i]$ 가 i를 중심으로 하는 최장 홀수 길이의 팰린드롬이 됩니다.

예를 들어 bananac로 A 배열을 만든다고 했을 때 $A_4$ 는 문자 n을 중심으로 하는 홀수 팰린드롬 중 가장 긴 팰린드롬은 ana이므로 이의 반지름에 해당하는 1이 됩니다. 이렇게 값을 채워보면 아래와 같습니다.

![](https://contents.codetree.ai/problems/3409/images/introductions-74fa0f51-4979-48d9-8d11-81b38e3d5cb4.png)

이렇게 값을 채우게 되면 주어진 문자열 내 최대 홀수 팰린드롬의 길이는 $2A_i + 1$ 중 최댓값을 구하는 것으로 계산이 가능합니다.

$A$ 를 계산하는 가장 간단한 방법은 맨 처음 위에서 소개했던 것처럼 각 위치를 중심으로 하여 양쪽 경계에 있는 문자가 일치하는 한 최대로 뻗어나가보는 것입니다. 이 방법에는 $O(N^2)$ 의 시간이 소요됩니다.

```python
input_str = "bananac"

# Manacher's algorithm을 진행해봅니다.
n = len(input_str)
A = [0] * n
for i in range(n):
    # 0에서 시작합니다.
    A[i] = 0

    # i를 중심으로 최대로 뻗어나갑니다.
    while i - A[i] - 1 >= 0 and i + A[i] + 1 < n and \
          input_str[i - A[i] - 1] == input_str[i + A[i] + 1]:
        A[i] += 1 

# 최장 홀수 팰린드롬의 길이를 계산합니다.
ans = 0
for i in range(n):
    ans = max(ans, 2 * A[i] + 1)

print(ans) # 5
```

여기서 시간을 줄일 수 있는 방법이 있습니다. A값을 순서대로 채우고 있던 상황이라고 생각해봅시다. 즉, $A_0, A_1, ..., A_{i-1}$ 까지는 전부 값을 구해놓았고 이제 $A_i$ 를 구해야 하는 상황이라고 가정해봅시다.

$A_0, A_1, ..., A_{i-1}$ 중 $i+A_i$ 값이 가장 컸을 경우의 i를 p, 그때의 $i+A_i$ 값을 r이라 해봅시다. 그러면 r은 $p+A_p$ 가 됩니다. **이때 만약 r이 i보다 크다면 아래와 같은 그림을 그려볼 수 있습니다.**

![](https://contents.codetree.ai/problems/3409/images/introductions-abb02aee-430a-4f09-bf5d-dfbdd993cfb8.png)

i를 p에 대칭시켰을 때의 위치를 ii라 한다면, p를 기준으로 반지름 $A_p$ 만큼 팰린드롬이기에 아래 초록색 영역은 서로 대칭이 됩니다.

![](https://contents.codetree.ai/problems/3409/images/introductions-7fa80047-1932-4c8b-964b-643fbebfd9be.png)

순서대로 A값을 구한 상황이므로 $A_{ii}$ 는 이미 알고 있습니다. 만약 $A_{ii} > r - i$ 를 만족한다면 i를 중심으로 초록색 영역 만큼은 확실히 팰린드롬임을 확신할 수 있기에 **$A_i$ 를 $r-i$** 를 시작으로 하여 확장시켜주는 식으로 시간을 줄일 수 있습니다.

![](https://contents.codetree.ai/problems/3409/images/introductions-70c26e16-3d23-4607-92ba-1c51b26e2274.png)

만약 $A_{ii} \le r - i$ 를 만족한다면 i를 중심으로 파란색 영역 만큼은 확실히 팰린드롬임을 확신할 수 있기에 **$A_i$ 를 $A_{ii}$** 를 시작으로 하여 확장시켜주는 식으로 시간을 줄일 수 있습니다.

![](https://contents.codetree.ai/problems/3409/images/introductions-8ad02e16-2844-41ff-ade8-5263e37c1a47.png)

즉, r이 i보다 작다면 원래대로 $A_i$ 를 0부터 확장하는 것을 진행해야 하지만, 만약 **r이 i보다 같거나 큰 상황에 대해서는 $A_i$ 를 $min(r - i, A_{ii})$ 부터 시작하여 확장하는 식으로 진행이 가능합니다.**

이 방식을 이용하면 놀랍게도 시간복잡도 $O(N)$ 에 A 배열을 전부 채워줄 수 있게 됩니다. 상황에 맞는 r, p 값은 $A_i$ 가 정해짐과 동시에 바로 $O(1)$ 에 갱신이 가능하므로 쉽게 계산이 가능합니다. 이렇게 최장 홀수 팰린드롬을 $O(N)$ 에 구할 수 있기 때문에, 주어진 문자열에 #을 붙여 최장 홀수 팰린드롬의 길이를 구한 뒤 그 답을 2로 나눈 몫을 구하면 문제에서 원하는 답을 $O(N)$ 에 구할 수 있습니다. 코드는 아래와 같습니다.

```python
# 주어진 문자열:
temp = "bananac"

# Manacher's algorithm을 적용하기 위해
# 주어진 문자열 내 문자 사이사이에 #을 넣어줍니다.    
input_str = "#" + "#".join(temp) + "#"

# Manacher's algorithm을 진행해봅니다.
n = len(input_str)

# A : i번지를 중심으로 하는 홀수 길이의 팰린드롬 중 
#     가장 긴 팰린드롬의 반지름의 길이
# 즉, [i - A[i], i + A[i]]가 i를 중심으로 하는 최장 팰린드롬이 됩니다.
A = [0] * n
r, p = -1, -1
# r : j < i를 만족하는 j들 중 max(j + A[j]) 값을 기록합니다.
# p : max(j + A[j]) 가 되는 j의 값을 기록합니다.
for i in range(n):
    # 만약 r값이 i보다 작다면
    # 줄일 수 있는 부분이 없으므로
    # A[i] = 0으로 시작합니다.
    if r < i:
        A[i] = 0
    # r값이 i보다 같거나 크다면
    # i를 p로부터 대칭시켰을 때의 위치인 ii에 대해
    # 이미 계산된 A[ii]값을 이용하여
    # i를 중심으로 뻗어나갈 수 있는 적절한 초기값을 
    # O(1)에 정해줄 수 있습니다.
    else:
        ii = 2 * p - i
        A[i] = min(r - i, A[ii])

    # i를 중심으로 최대로 뻗어나갑니다.
    while i - A[i] - 1 >= 0 and i + A[i] + 1 < n and \
          input_str[i - A[i] - 1] == input_str[i + A[i] + 1]:
        A[i] += 1 

    # i + A[i] 중 최대가 선택되도록
    # r, p값을 갱신해줍니다.
    if i + A[i] > r:
        r, p = i + A[i], i

# 최장 팰린드롬의 길이를 계산합니다.
ans = 0
for i in range(n):
    ans = max(ans, 2 * A[i] + 1)

# 처음 주어진 문자열에서 
# #을 제외한 부분의 길이가 실제 답이 되기에
# 2로 나눴을 때의 몫이 답이 됩니다.
print(ans // 2)
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.