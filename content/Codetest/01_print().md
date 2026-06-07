---
tags:
  - "#print"
  - "#join"
  - "#end"
---


## 01. print / end = " "

```python
for i in range(10):
  print(i, end='')

print(10)
# ----------------------

# 012345678910

```

print(, end)를 사용하고 다음에 print을 진행하면 연속해서 붙게 됩니다.

코테를 푸는 과정에서 

## 02. print / join()

```python
# join

print(' '.join(str(i) for i range(10)))
print(10)

# -----------------------
01232456789
10


# print() + end
# -----------------------
for i in range(10):
  print(i, end=' ')
print()
print(10)

# -----------
0 1 2 3 4 5 6 7 8 9 
10



```


## 03. print() / *

```python
n = 4
arr = [[0]*n for _ in range(n)]

arr

# -----------------
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

# -----------------

for row in arr:
  print(*row)

# -----------------

0 0 0 0
0 0 0 0
0 0 0 0
0 0 0 0

```