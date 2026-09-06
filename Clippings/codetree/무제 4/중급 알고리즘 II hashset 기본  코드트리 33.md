---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-substring-occurrence-count/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 3. KMP

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## Knuth–Morris–Pratt (KMP) Algorithm

Rabin Karp 알고리즘을 이용하면 길이가 각각 n, m인 두 문자열 T(=text), P(=pattern)가 주어졌을 때 문자열 T의 부분 문자열 중 문자열 P와 일치하는 경우가 있는지를 $O(N + M)$ 에 구할 수 있다고 했습니다. 이렇게 부분 문자열로서 어디에서 일치하는지를 $O(N + M)$ 에 찾아낼 수 있는 또 다른 알고리즘이 있습니다. 바로 KMP Algorithm 입니다.

KMP Algorithm은 String Hashing 기법과는 다르게 정확히 한 문자열이 다른 문자열의 부분 문자열로 나타나는지를 판단하는 데에만 활용되고는 합니다. 단, KMP에서 사용되는 Failure Function 개념은 다양한 알고리즘에서 활용되기에 잘 알아놓으시는 것을 추천드립니다.

## 실패 함수

KMP Algorithm을 이해하기 위해서는 먼저 Failure Function 이라는 실패 함수에 대해 알아봐야 합니다.

KMP Algorithm에서의 실패 함수 f는 배열로 나타내어 지며, f\[i\]는 `문자열 P에서 [1, i]로 이루어진 문자열 중 접두사와 접미사가 일치하는 최장 길이를 뜻합니다. 단, 이때 자기 자신은 제외합니다.`

예로 T와 P가 각각 "ABABABBABABABC", "ABABABC"인 경우에 대해서 생각해봅시다.

P로부터 완성되는 f는 아래와 같습니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-fd39be78-1f3c-4683-ae37-d042d3dc5f7e.png)

KMP에서 중요한 것은 T, P 모두 1번지부터 사용해야 코드 작성에 용이하다는 것입니다. 또, 정의되지 않는 f\[0\]에 대해서는 -1을 넣어주는 것이 코드 작성에 도움이 되니 꼭 기억해주세요.

예로 f\[3\]은 "ABA"에서 접두사와 접미사가 일치하는 최장 길이(자기 자신 제외)이므로 "A"가 되어 1이 됩니다. 또, f\[5\]는 "ABABA"에서 접두사와 접미사가 일치하는 최장 길이이므로 "ABA"가 되어 3이 됩니다.

이러한 f값을 무작정 완전탐색을 이용해 채우려고 하면, 문자열 P의 길이를 L이라 했을 때 $O(M^3)$ 의 시간이 소요됩니다. 이를 $O(M)$ 으로 줄일 수 있는 방법이 있습니다. 바로 그 전까지 채워진 f를 이용하는 것입니다.

f값은 증가하는 순으로 하나씩 채워질 것입니다. 먼저 아래와 같이 f\[0\] ~ f\[5\]까지 채워진 상황에서 f\[6\]을 어떻게 채울 것인지에 대해 생각해보겠습니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-d95be5eb-d966-40c7-a4b1-8c89d5778d6e.png)

f\[5\]는 정의상 "ABABA"에서 접두사와 접미사가 일치하는 최장 길이인 3이 됩니다. 현재 채워야 하는 위치를 i, \[1, i - 1\]로 이루어진 문자열에서 접두사와 접미사가 일치하는 최장 길이에 해당하는 f\[i - 1\]값을 j라고 표시해보겠습니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-b9659793-e036-487c-97f7-96bb8636b576.png)

우리의 전략은 **\[1, i - 1\]까지의 문자열의 접두사와 접미사가 일치하는 길이를 큰 것부터 조회하는 것입니다.** 여기서 처음 j는 3이고, P\[i\]와 P\[j + 1\]이 일치하기에 f\[6\]은 j + 1에 해당하는 4로 결정됩니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-1059e06c-b9aa-4650-ad51-64e90210abc5.png)

이제 f\[7\]을 채우는 경우에 대해서 생각해보겠습니다. i = 7, j = 4(=f\[i - 1\])에서 시작됩니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-e89cf8b4-ae69-46f2-8bb4-8ce0dbba3792.png)

우리의 전략은 \[1, i - 1\]까지의 문자열의 접두사와 접미사가 일치하는 길이를 큰 것부터 조회하는 것이라고 했습니다. i = 7, j = 4일 때 P\[i\]와 P\[j + 1\]은 일치하지 않습니다. 따라서 j 값에는 변화가 필요합니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-c1c2f17c-d20b-445e-b86e-29cad1a64763.png)

j가 처음 4였던 이유는 \[1, i - 1\]까지의 문자열의 접두사와 접미사가 일치하는 최장길이가 4이기 때문입니다. 이제 \[1, i - 1\]까지의 문자열의 접두사와 접미사가 일치하는 경우 중 그 다음으로 긴 길이를 찾아야 합니다.

**그런데 잘 생각해보면, 그 다음 j는 바로 f\[j\]값이 됩니다.** 그 이유는 생각보다 간단합니다.

지금 찾아야 할 next j는 아래와 같이 \[1, i - 1\]까지의 문자열의 접두사와 접미사가 일치하는 경우 중 그 다음으로 긴 길이입니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-020e6fb8-6b1f-4d13-a04e-f035eaa14e4b.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-41bee99f-b5cd-4ef7-8800-40a85464e233.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-b7f63cde-4c13-4938-a357-af4b5a6e5e4d.png)

1 / 3

이때 초록색 영역은 동일한 문자열이므로 우측에 있는 파란색 영역이 좌측 영역으로 넘어올 수 있게 되고, 이는 곧 \[1, j\]까지의 문자열의 접두사와 접미사가 일치하는 최장길이를 찾는 문제가 되므로 바로 f\[j\]가 우리가 찾던 next j가 됩니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-3efe6c7f-d0c3-40f0-a5cd-a75cf678dc97.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-33d46ba5-8976-47f5-9e71-6038c6a1c0f0.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-293d336c-a481-4506-8542-713c6ae90c14.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-50411ebc-c074-4522-8bb7-2af26937e052.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-bd3a4ba4-6fe4-4281-bf70-91bcc178b36a.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-ed88e021-7ae8-4af0-b577-50ef6ea53198.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-b5e42bdb-4a08-40a8-b05e-ea3019f72392.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-0aa19d15-dc56-436c-8bf8-be0a9da2fcc2.png)

1 / 8

따라서 i = 7, j = 4일 때 P\[i\]와 P\[j + 1\]은 일치하지 않기에 그 다음 j는 아래와 같이 f\[4\]인 2가 됩니다.

i = 7, j = 2일때에도 P\[i\]와 P\[j + 1\]은 일치하지 않습니다. 따라서 다시 j는 f\[2\]에 해당하는 0이 됩니다.

i = 7, j = 0일때에도 P\[i\]와 P\[j + 1\]은 일치하지 않습니다. 이 경우 j는 f\[0\]에 해당하는 -1이 됩니다. j가 음수가 되면 매칭이 아예 실패했다는 뜻이기에, 이때는 그대로 종료가 됩니다. 따라서 f\[7\]은 j + 1에 해당하는 0으로 결정됩니다.

이 과정을 통해 f를 채우면 놀랍게도 $O(M)$ 의 시간이 걸립니다. 그 이유는 j가 1씩 증가하기 위해서는 최소 i가 1씩은 증가해야만 하기 때문에 j는 최대 M번 증가가 가능하므로 i, j가 같이 움직인다 하더라도 독립적으로 i, j는 최대 $O(M)$ 번 움직이게 되기 때문입니다.

f를 채워넣는 코드는 아래와 같습니다.

```python
text = "ABABABBABABABC"
pattern = "ABABABC"

n = len(text)
m = len(pattern)

# failure function입니다.
# f[i] : pattern에서 
#        [1, i]로 이루어진 문자열 중
#        접두사와 접미사가 일치하는 최장 길이 (단, 자기자신은 제외)
f = [0] * (m + 1)

# 구현의 편의를 위해 맨 앞에 #을 붙여
# 문자열을 1번지부터 사용합니다.
text = "#" + text
pattern = "#" + pattern

# failure function값을 먼저 계산합니다.
f[0] = -1 # f[0]은 구현의 편의를 위해 -1로 설정합니다.
for i in range(1, m + 1):
    # 시작은 최적의 답에 해당하는 f[i - 1]에서 합니다.
    # 그 전 위치까지 최적의 (접두사, 접미사) 매칭 결과 바로 뒤에
    # 추가되는 것이 가능하다면 최적의 답이 되기 때문입니다.
    j = f[i - 1]
    # [1, i - 1]까지는
    # 정확히 길이 j만큼 접두사와 접미사가 일치한다고 했을 때
    # 그 다음 문자인 pattern[j + 1]과 pattern[i]가 일치하는지를 확인합니다.
    # 일치하지 않는다면 그 다음 후보로 j값을 옮겨줍니다.
    while j >= 0 and pattern[j + 1] != pattern[i]:
        j = f[j]

    # [1, i - 1]까지 일치하며 동시에 그 다음 문자까지 일치하는 최대 j가 구해져있으므로
    # 이제 그 값에 1을 더한 결과가 f[i]가 됩니다.
    # 매칭에 실패했더라도 f[0]에는 -1이 들어있기에
    # f[i] = 0이 됩니다.
    f[i] = j + 1
```

## 부분 문자열 매칭

이제 f가 완성되었으니 문자열 T와 문자열 P간의 문자열 매칭을 진행할 수 있습니다. **i는 현재 매칭시켜야 하는 문자열 T의 index이고, j는 문자열 T의 i - 1까지 문자열 P을 매칭시킬 수 있는 경우에 해당하는 문자열 P의 index가 됩니다.** i = 1, j = 0에서 시작하며, 정의상 T\[i\]와 P\[j + 1\]이 일치하면 전진시에는 항상 i, j 모두 1씩 증가하게 됩니다.

![](https://contents.codetree.ai/problems/3418/images/introductions-2ba532c8-759e-4d32-a5d5-e21a5743b399.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-9bc008c7-9776-4714-9b44-f7b11152d4f8.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-f6952017-9688-4717-935d-87278c4a60c0.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-9c5ccc48-ddae-4324-b1b2-34be6678c0d6.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-5f45c7f9-ec13-4bc9-a1a2-9f63bd8abca9.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-44c19d7b-3d51-465b-bbda-ca591c0d1ab6.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-33584881-8457-42a0-92c9-dd34232d8636.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-9e6647aa-1be0-4d03-92ea-fefc5bfd11e8.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-399c2898-3521-49e6-9586-5025f42107d1.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-dc9187af-7623-4cc1-aaf6-e78f316897e7.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-4dc4339b-e63c-45ff-85bc-666335defc0e.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-ee67ddc3-0d41-4d82-89f4-cfda0001c521.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-669bfe12-8457-40e8-93aa-4e5ba836e811.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-f17a1846-26de-4c43-bc13-26f80991dea1.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1112a583-a570-418e-bbb3-7b13dc02e102.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-a8c23ed3-7d0b-4b35-99ba-273830903229.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-e199d4d4-d38f-48d4-ab1a-2a4324528773.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-d40c6fc2-6c6e-497f-bc9a-a96f17e0ba64.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-d45d5c84-0ae8-4f68-92d7-fa7d4597ff44.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-51e78262-7221-4054-bb84-6594374e18db.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-84f58c35-635c-4d66-b336-1a79d5efef6e.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-bc59b5d8-24e7-4f58-bd26-22d490d0acdd.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-0b1b34c5-4848-4dfd-b502-277137c22b93.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-2b9c8656-dd97-4eef-9f30-37e34f3a4853.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-d39cda92-4a66-43c0-a7d3-43a832987d0e.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-e4bd522c-e90b-452d-bb15-14281060db6b.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-6f97f412-b851-4865-84dd-2302d0f64a32.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-0b17ad9e-b032-485c-8604-2e7006954920.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-cc8a1ea6-edc2-416e-a549-dea2a05c82c9.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-7f550dfd-9162-48db-a3c7-aea6875d08e5.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-204c0b47-59c6-41e7-bf11-1b65bc69ddb0.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1a5f77d1-c367-419b-b3a6-7f20e3b0ee0a.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-491aae78-5524-4b07-9096-0dd80ea3416c.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-cbd8503c-42d9-4632-9557-54b522db6a19.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-4a6fc337-1a34-474c-9a72-9569549a28ae.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-f2d1c19e-377f-4c63-a8fc-cf2772540cdb.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-cf7ce086-e5db-4d87-a0d5-d41b1ec4c28d.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-63d1e8ee-09ef-415e-8601-c9cb8333e1f2.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-d798b67c-8050-4ec0-bee0-549039ecab27.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-bec33521-a8fb-47f2-9749-7991ea192423.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1db25712-d0f8-4117-9c56-f7d3499b13d6.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-7c748ff5-b924-4d02-b70c-153418ac40db.png)

1 / 42

i = 7, j = 6일 때 T\[i\]와 P\[j + 1\] 값이 달라지게 됩니다. **이때의 대응도 f를 채울 때와 아예 동일합니다.**

j는 문자열 T의 i - 1까지 문자열 P을 매칭시킬 수 있는 경우에 해당하는 문자열 P의 index가 됩니다. 최장으로 매칭시키는 것이 좋기에 가능한 경우 중 최대인 경우부터 j에 넣어주는 것이 중요합니다.

T\[i\]와 P\[j + 1\]이 다른 값을 갖기 때문에, 이제 문자열 T의 i - 1까지 문자열 P을 매칭시킬 수 있는 경우 중 그 다음으로 큰 j를 찾아야 합니다.

**여기서도 f를 채울 때와 마찬가지 이유로 그 다음 j는 바로 f\[j\]값이 됩니다.** 즉, 그 다음 j는 f\[6\]에 해당하는 4로 바뀌게 됩니다.

i = 7, j = 4일 때 역시 T\[i\]와 P\[j + 1\] 값이 다르기 때문에 j는 다시 f\[4\]인 2가 되고, i = 7, j = 2일 때 역시 T\[i\]와 P\[j + 1\]값이 다르기 때문에 j는 다시 f\[2\]인 0이 되고, i = 7, j = 0일 때에도 값이 다르기에 j = -1이 되며 음수가 되어 비교가 종료됩니다. 이렇게 -1이 되었을 경우에는 매칭이 실패했을 경우가 됩니다.

그 다음 이제 전진을 해야하므로 i, j가 1씩 증가된 상태로 계속 매칭을 이어가게 됩니다. 즉, i = 8, j = 0부터 다시 매칭이 시작됩니다.

이렇게 계속 진행을 하다보면 결국 **j가 m이 되는 경우** 가 있는데, 이때는 문자열 P가 문자열 T에 부분문자열로서 정확히 매칭이 되었다는 뜻이 됩니다.

## 매칭 성공 후

아래 영상을 보면,

![](https://contents.codetree.ai/problems/3418/images/introductions-8f49b03e-d3b3-40c0-b995-9f9f18449d95.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-0d706994-4a0d-4df9-b46d-86900251b47e.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-212c47f5-e21d-4b1b-9d16-2765e66068fd.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1c7d5f67-42e8-4865-9b1e-178d92c0c475.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-548d75ae-8e5f-40e3-9afe-a3b65a319854.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-f42a8285-d4c5-482d-8118-933a95becd7c.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-cf4d07b5-37ab-48f3-a258-ec93aac7b50b.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-da89ed82-dea3-4a65-b36f-39c70726d3c0.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-140c67b4-ee66-4270-9a94-82c0cc3536a6.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-60b7ae5a-3d2a-4f0a-9b0d-7b3a60bedab2.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-b555169b-f261-473c-b456-3858b567b3bf.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-281ff782-b18b-4728-bc84-d81755b83b0d.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-8158c033-200e-48fd-8034-d22950c49ccf.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-62bf39e8-2ce7-4e9f-9d0f-f35d23b3c1a3.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1e2818fe-e619-486c-841e-55aa465ea8fd.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-23fa05e6-5c81-415b-aad1-569b3de6d2dc.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-219d0b56-5e83-41c6-b61f-f490d2ba32b2.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-537f4ad5-1406-4475-87d4-fa89a3da3d9b.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-b67c49c4-0c61-49ce-921d-9f6722502322.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-0125947b-0f6b-4468-902e-eb1ed8c6c0f0.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-1cef6997-c9b7-4634-9eb3-4c6404d174c8.png) ![](https://contents.codetree.ai/problems/3418/images/introductions-31e5df0f-c3cd-4b73-9eea-4105a2196e0d.png)

1 / 22

이렇게 매칭이 된 직후에는 다른 곳에서 매칭이 되는 곳을 추가적으로 탐색하기 위해 j값을 f\[j\]로 변경하여 추가적으로 더 탐색을 이어나가야 함에 유의합니다.

매칭 과정에 있어서도 시간복잡도는 놀랍게도 $O(N)$ 이 됩니다. 그 이유는 f를 채울 때와 마찬가지로 j가 1씩 증가하기 위해서는 최소 i가 1씩은 증가해야만 하기 때문에 j는 최대 N번 증가가 가능하므로 i, j가 같이 움직인다 하더라도 독립적으로 i, j는 최대 $O(N)$ 번 움직이게 되기 때문입니다.

따라서 KMP의 총 시간복잡도는 $O(N + M)$ 이 됩니다.  
전체 KMP 코드는 아래와 같습니다.

```python
text = "ABABABBABABABC"
pattern = "ABABABC"

n = len(text)
m = len(pattern)

# failure function입니다.
# f[i] : pattern에서 
#        [1, i]로 이루어진 문자열 중
#        접두사와 접미사가 일치하는 최장 길이 (단, 자기자신은 제외)
f = [0] * (m + 1)

# 구현의 편의를 위해 맨 앞에 #을 붙여
# 문자열을 1번지부터 사용합니다.
text = "#" + text
pattern = "#" + pattern

# failure function값을 먼저 계산합니다.
f[0] = -1 # f[0]은 구현의 편의를 위해 -1로 설정합니다.
for i in range(1, m + 1):
    # 시작은 최적의 답에 해당하는 f[i - 1]에서 합니다.
    # 그 전 위치까지 최적의 (접두사, 접미사) 매칭 결과 바로 뒤에
    # 추가되는 것이 가능하다면 최적의 답이 되기 때문입니다.
    j = f[i - 1]
    # [1, i - 1]까지는
    # 정확히 길이 j만큼 접두사와 접미사가 일치한다고 했을 때
    # 그 다음 문자인 pattern[j + 1]과 pattern[i]가 일치하는지를 확인합니다.
    # 일치하지 않는다면 그 다음 후보로 j값을 옮겨줍니다.
    while j >= 0 and pattern[j + 1] != pattern[i]:
        j = f[j]

    # [1, i - 1]까지 일치하며 동시에 그 다음 문자까지 일치하는 최대 j가 구해져있으므로
    # 이제 그 값에 1을 더한 결과가 f[i]가 됩니다.
    # 매칭에 실패했더라도 f[0]에는 -1이 들어있기에
    # f[i] = 0이 됩니다.
    f[i] = j + 1

# 한 문자씩 비교하며 패턴 문자열과 일치하게 되는 순간을 구합니다.
j = 0
for i in range(1, n + 1):
    # text의 [i - j, i - 1]와 pattern의 [1, j]가 일치한다는 가정 하여
    # 그 다음 문자인 pattern[j + 1]와 text[i]를 비교합니다.
    # 일치하지 않는다면 f를 이용하여 그 다음 후보로 j값을 빠르게 옮겨줍니다.
    while j >= 0 and pattern[j + 1] != text[i]:
        j = f[j]
    
    # 일치하는 곳에서 빠져나온 것이기에
    # 이제 j를 1만큼 증가시킵니다.
    # 매칭에 실패했더라도 j = -1에서 끝났을 것이기에
    # 그 다음 j는 0이 됩니다.
    j += 1
    
    # j가 m이 되면 전부 일치했다는 뜻이므로 
    # 답을 갱신해주고 다시 그 다음 후보로 넘어갑니다.
    if j == m:
        print(f"matched at {i}th index!")
        j = f[j]
```

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.