

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



![[Pasted image 20260607235025.png]]


## choose()

```python
n = 3
answer = []

def print_answer():
    for elem in answer:
        print(elem, end=" ")
    print()

def choose(curr_num):
    # 종료 조건
    if curr_num == n + 1:
        print_answer()
        return
    
    # 0을 선택했을 때 재귀 호출
    answer.append(0)
    choose(curr_num + 1)
    answer.pop()

    # 1을 선택했을 때 재귀 호출
    answer.append(1)
    choose(curr_num + 1)
    answer.pop()

    return

choose(1)
```

## choose() / range
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