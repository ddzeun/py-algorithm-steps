## 배열을 다룰 때 알아두면 좋은 문법

---

## 1. **리스트 생성 & 초기화**
```python
# 0으로 채운 리스트
arr = [0] * n

# 1~n까지 채운 리스트
arr = list(range(1, n+1))

# 2차원 배열 초기화
arr = [[0]*m for _ in range(n)]
```
> 기본 리스트 만들기 패턴

---

## 2. **리스트 슬라이싱**
```python
arr = [1, 2, 3, 4, 5]
arr[1:4]        # [2, 3, 4]
arr[::-1]       # [5, 4, 3, 2, 1]
arr[1:4][::-1]  # [4, 3, 2]
```
> `arr[i:j]`는 i 포함, j 제외

---

## 3. **리스트 뒤집기**

| 방법 | 코드 | 특징 |
|------|------|------|
| in-place | `arr.reverse()` | 원본 자체를 뒤집음 |
| 새 리스트 | `arr[::-1]` | 복사된 역순 리스트 반환 |
| iterator | `reversed(arr)` | 지연 평가 (iterator 반환) |

---

## 4. **정렬**
```python
arr.sort()           # 오름차순 정렬 (in-place)
arr.sort(reverse=True)  # 내림차순

sorted_arr = sorted(arr)  # 원본 유지, 새 리스트 반환
```
> arr.sort()는 원본 정렬, sorted()는 복사본 생성


**key 함수 사용**

```python
arr = ['apple', 'banana', 'kiwi']

# 길이 기준 정렬
arr.sort(key=len)

# 절댓값 기준 정렬
arr2 = [-3, 1, -7, 4]
arr2.sort(key=abs)
```

---

## 5. **리스트 탐색**
```python
# 값 존재 여부
if x in arr:
    ...

# 인덱스 찾기
arr.index(x)  # 없으면 ValueError 발생

# 특정 조건 필터링
even = [x for x in arr if x % 2 == 0]
```
> `in`, `index()`, 리스트 컴프리헨션 활용

---

## 6. **리스트 변환 (comprehension)**
```python
# 제곱 리스트
squared = [x**2 for x in arr]

# 조건 있는 변환
filtered = [x for x in arr if x > 0]
```
> 꼭 기억하기

---

## 7. **리스트에 값 추가 / 삭제**
```python
arr.append(10)     # 맨 뒤에 추가
arr.insert(2, 20)  # 특정 위치에 삽입
arr.pop()          # 마지막 요소 제거
arr.pop(1)         # 인덱스 1 제거
arr.remove(5)      # 값 5 제거 (처음 등장하는 것만)
```
> append, insert, pop, remove 조합 기억

---

## 8. **누적합 (Prefix Sum)**
```python
arr = [1, 2, 3, 4]
prefix = [0]
for num in arr:
    prefix.append(prefix[-1] + num)

# 구간합 arr[i:j] → prefix[j] - prefix[i]
```
> 빠른 구간합 계산에 필수

---

## 9. **enumerate & zip**
```python
for i, val in enumerate(arr):
    print(i, val)

a = [1, 2, 3]
b = [4, 5, 6]
for x, y in zip(a, b):
    print(x + y)
```
> 인덱스가 필요하면 enumerate, 여러 리스트 동시에 돌 때 zip

---

## 10. **최대/최소 값 & 인덱스**
```python
max_val = max(arr)
min_val = min(arr)
idx = arr.index(max_val)
```
> max(), min(), index() 조합 활용

---

## 11. **리스트 복사 (copy)**
```python
# 얕은 복사 (새 리스트 생성)
copy_arr = arr[:]
copy_arr = arr.copy()

# deepcopy (2차원 이상 구조 복사할 때)
import copy
deep_copy_arr = copy.deepcopy(arr)
```
> 얕은 복사는 2차원 이상에서 '안쪽 리스트'까지는 복사 안 됨

---

## 12. **collections.Counter (빈도 세기)**
```python
from collections import Counter

arr = ['a', 'b', 'a', 'c', 'b', 'a']
counter = Counter(arr)

# 결과: Counter({'a': 3, 'b': 2, 'c': 1})
```
> `Counter`는 리스트 원소들의 등장 횟수를 딕셔너리처럼 저장해줌

---

## 13. **heapq (최소/최대 힙)**
```python
import heapq

# 최소 힙
heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 4)
heapq.heappop(heap)  # 1
```
> 기본은 최소 힙, 최대 힙은 음수 변환

---

## 14. **collections.deque (양방향 큐) 빠른 삽입/삭제**
```python
from collections import deque

dq = deque([1, 2, 3])
dq.append(4)
dq.appendleft(0)
dq.pop()
dq.popleft()
```
> 일반 리스트보다 **양쪽 삽입/삭제** 속도가 훨씬 빠름 (O(1))

---

## 15. **투 포인터 (Two Pointers)**
```python
arr = [1, 2, 3, 4, 5]
left, right = 0, len(arr) - 1

while left < right:
    total = arr[left] + arr[right]
    if total == target:
        break
    elif total < target:
        left += 1
    else:
        right -= 1
```
> **정렬된 배열**에서 두 포인터로 탐색할 때 자주 사용 (정렬된 배열에서 합 구할 때 필수)

---

## 16. **슬라이딩 윈도우 (Sliding Window)**
```python
arr = [1, 2, 3, 4, 5]
k = 3  # 윈도우 크기

window_sum = sum(arr[:k])
max_sum = window_sum

for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i - k]
    max_sum = max(max_sum, window_sum)
```
> 고정된 크기의 구간합/최댓값/최소값 구할 때 많이 사용

---

## 17. **2차원 배열 순회**
```python
arr = [
    [1, 2, 3],
    [4, 5, 6]
]

for i in range(len(arr)):
    for j in range(len(arr[0])):
        print(arr[i][j])
```

> 기본적으로 `행 먼저, 열 나중에` 순회하

---

## 18. **2차원 배열 누적합 (Prefix Sum 2D)**
```python
n, m = 3, 3
arr = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

prefix = [[0]*(m+1) for _ in range(n+1)]

for i in range(1, n+1):
    for j in range(1, m+1):
        prefix[i][j] = arr[i-1][j-1] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]

# (1,1)부터 (x,y)까지의 합 = prefix[x][y]


# (r1,c1) ~ (r2,c2) 구간합
# prefix[r2][c2] - prefix[r1-1][c2] - prefix[r2][c1-1] + prefix[r1-1][c1-1]
```
> 빠른 2차원 구간합, 사각형 범위의 합 구할 때 사용

---