---
tags:
  - 오답노트
  - "#Medium"
  - "#해결"
  - "#완전탐색"
source: https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-G-or-H-2/description
created:
---
## 목차
[[#1. 문제]]
[[#2. 입력 & 출력 & 예제]]
[[#3. 접근 방법]]
[[#4. 주의할 점]]


## 0. 해결 & 해설
1. 에외 처리가 너무 힘들다.
2. 시험 볼때에는 이것을 확인하지 못한다.
3. 스스로 예외인 경우까지 생각을 해야한다.
4. 슈도 코드를 제대로 작성해보자
5. 그래도 접근 방법은 맞았느뎨
6. 조건에 만족할때 구간의 길이를 구하는 방법이 틀렸다.
> [!example]-
> ![[Pasted image 20260616154755.png]]
> ![[Pasted image 20260616154804.png]]


```python
MAX_NUM = 100

# 변수 선언 및 입력
n = int(input())
arr = [0] * (MAX_NUM + 1)

for _ in range(n):
    x, c = tuple(input().split())
    x = int(x)
    
    arr[x] = 1 if c == 'G' else 2

# 모든 구간의 시작점을 잡아봅니다.
max_len = 0
for i in range(MAX_NUM + 1):
	for j in range(i + 1, MAX_NUM + 1):
		# i와 j 위치에 사람이 있는지 확인합니다.
		if arr[i] == 0 or arr[j] == 0:
			continue
		
		# 해당 구간 내 g와 h의 개수를 구합니다.
		cnt_g = 0
		cnt_h = 0
		
		for k in range(i, j + 1):
			if arr[k] == 1:
				cnt_g += 1
			if arr[k] == 2:
				cnt_h += 1
		
		# 조건을 만족할 때 구간의 길이를 구해 최댓값과 비교합니다.
		if cnt_g == 0 or cnt_h == 0 or cnt_g == cnt_h:
			leng = j - i
			max_len = max(max_len, leng)

print(max_len)

```




## 1. 문제
![[Pasted image 20260616154954.png]]

----
## 2. 입력 & 출력 & 예제

![[Pasted image 20260616155008.png]]
![[Pasted image 20260616155018.png]]

----

## 3. 접근 방법

### 1. 슈도코드
이렇게 접근했지만
오류 처리는 코드 실행을 바탕으로 진행함..
즉........ 오류인지는 확인 가능하지만
무슨 값에서 틀렸는지는 실제에서는 확인하기 힘들다.

```

# n 입력
# range(n) 만큼 위치 및 g, h 입력
# value = [0]*101 만들기
# 위치에 넣기


# 사진 크기는 양쪽 끝에 있는 사람 간의 거리
# 1 2 => 2-1 크기 1
# 1 => 크기 0


# lst = [] 
# for i in range(102):
    # if value[i] != 0:
    #   lst.append(value[i])


# for i in lst:
# for j in lst:
# cnt G, cnt h 같은 때
# 구하는 거야

# i, j 구하는 거지
```

----

## 4. 주의할 점

1. 에외 처리가 너무 힘들다.
2. 시험 볼때에는 이것을 확인하지 못한다.
3. 스스로 예외인 경우까지 생각을 해야한다.
4. 슈도 코드를 제대로 작성해보자

----
