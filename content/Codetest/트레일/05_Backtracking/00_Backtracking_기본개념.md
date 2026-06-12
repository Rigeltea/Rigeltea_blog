

## choose 정리

```python

def choose(idx):

	if idx == 6:
	  return
	
	# 1 리스트 값 추가하기
	for i in range(4):
	  answer.append(i)
	  choose(idx+1)
	  answer.pop()
	  
	
	# 2 O or X
	# i가 들어가는 경우
	answer.append(i)
	choose(idx+1, selected)
	answer.pop()
	
	# i 가 들어가지 않는 경우
	choose(idx+1)
	
	
	# 3 value[]/ 리스트 안에 값 넣기
	for i in range(1,5):
	  value[idx] = i
	  choose(idx+1)
	



```





## 1. 재귀

![[Pasted image 20260607235007.png]]

```python
def get_sum(n):
    # 종료 조건
    if n == 1:
        return 1

    # 재귀 호출
    return n + get_sum(n - 1)

n = 5
print(get_sum(n))
```

## 2. Choose() / ```answer = []``` 리스트 안에 값 넣는 경우

![[Pasted image 20260607235025.png]]

### choose() / range
```python
def choose(curr_num):
    # 종료 조건
    if curr_num == n + 1:
        print_answer()
        return
    
"""
    # 0을 선택했을 때 재귀 호출
    answer.append(0)
    choose(curr_num + 1)
    answer.pop()

    # 1을 선택했을 때 재귀 호출
    answer.append(1)
    choose(curr_num + 1)
    answer.pop()
"""

    # 반복문을 이용해 0, 1을 선택했을 때 재귀 호출
    for select in range(2):
        answer.append(select)
        choose(curr_num + 1)
        answer.pop()

    return
```



## 3. choose() //  idx, selected / O&X / 2^n

```python

answer =

 
def choose(idx, selected):
    global ans
	
	# 상황에 따라 다르게 들어가
	
	if idx == n:
		return
	
	if len(selected) >= answer:
		return
	
	
	# idx 사용
	selected.append(idx)
	choose(idx+1, selecetd)
	selected.pop()
	
	# idx 사용하지 않음
	choose(idx+1 ,selected)	
	
	

choose(0, [])
```


###  예제 코드

예제 1번과 2번의 차이점은
2번은 그냥 사용해/ 사용하지 말아
이런 느낌이라며ㅏㄴ

1번 같은 경우는 사용해/ 사용하지 말아 
플러스 사용하는데 조건문이 들어갑니다. 그걸 포함해서 사용한 경우 입니다.

사용하는게 조건이 있기 때문에 
1번 같은 경우에는 사용하지 않는 것을 기준으로 들어가고

2번 같은 경우는 사용해 라는 조건 부터 들어갔습니다.
사용하지 말아 이것으로 시작해도 상관은 없음


우리는 그렇기 때문에 문제를 상황에 따라서
먼저 사용하는 경우와
사용하지 않는 경우를 고려 해야 할 필요가 있다.


#### 1. [[03_겹치지 않게 선분 고르기]] 정답코드
```python

n = int(input())

segments = []
for _ in range(n):
    l, r = map(int, input().split())
    segments.append((l, r))

ans = 0

def overlap(a, b):
    l1, r1 = a
    l2, r2 = b

    # 끝점을 공유해도 겹친다고 했으므로
    # 안 겹치려면 한 선분이 완전히 왼쪽에 있어야 함
    return not (r1 < l2 or r2 < l1)




def choose(idx, selected):
    global ans

    if idx == n:
        ans = max(ans, len(selected))
        return

    # 1. 현재 선분을 고르지 않는 경우
    choose(idx + 1, selected)

    # 2. 현재 선분을 고르는 경우
    can_select = True
    for seg in selected:
        if overlap(segments[idx], seg):
            can_select = False
            break

    if can_select:
        selected.append(segments[idx])
        choose(idx + 1, selected)
        selected.pop()

choose(0, [])

print(ans)
```

#### 2. [[04_사다리 타기]] 정답 코드

```python
n, m = map(int, input().split())

lines = []
for _ in range(m):
    a, b = map(int, input().split())
    lines.append((a, b))

# b가 높이니까, 위에서 아래 순서로 정렬
lines.sort(key=lambda x: x[1])

def simulate(selected):
    result = [i for i in range(n)]

    for idx in selected:
        a, b = lines[idx]

        # a번 세로줄과 a+1번 세로줄 연결
        # 파이썬 인덱스는 0부터라서 a-1, a
        result[a - 1], result[a] = result[a], result[a - 1]

    return result


target = simulate(range(m))

answer = m

def choose(idx, selected):
    global answer

    if len(selected) >= answer:
        return

    if idx == m:
        if simulate(selected) == target:
            answer = min(answer, len(selected))
        return

    # idx번째 가로줄 사용
    selected.append(idx)
    choose(idx + 1, selected)
    selected.pop()

    # idx번째 가로줄 사용 안 함
    choose(idx + 1, selected)


choose(0, [])
print(answer)
```




## 4. choose() / ``` value[i] = num ``` 리스트 안에 값 채우는 방식

```python
value = [0] * 6 
def choose(idx): 
	if idx == 6: print(value) 
	return 
	
for num in range(1, 5):
	 value[idx] = num choose(idx + 1)
```

왜냐하면 `idx` 자체가 이미 위치를 뜻하기 때문이야.

```
idx = 0 → value[0] = a 값
idx = 1 → value[1] = b 값
idx = 2 → value[2] = c 값
```

여기서는 `pop()`이 필요 없어.

다음 숫자로 덮어쓰면 되기 때문이야.

```
value[idx] = 1
choose(idx + 1)

value[idx] = 2
choose(idx + 1)

value[idx] = 3
choose(idx + 1)

value[idx] = 4
choose(idx + 1)
```



