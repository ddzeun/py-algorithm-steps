
## 정렬 심화

## **1. 계수 정렬 (Counting Sort)**

* 범위가 작은 정수(예: 0\~10000)일 때 사용
* 시간 복잡도 `O(n + k)`로 빠름 (단, 메모리 ↑)

```python
arr = [4, 2, 2, 3, 1, 4]
count = [0] * (max(arr) + 1)

for num in arr:
    count[num] += 1

sorted_arr = []
for i in range(len(count)):
    sorted_arr.extend([i] * count[i])  # 등장 횟수만큼 append
```

> 음수 포함 시: offset 조정 필요 (`count[num + abs(min_val)]` 등)

---

## **2. 객체(클래스) 정렬 – `__lt__` 오버라이드**

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __lt__(self, other):
        return self.score > other.score  # 점수 내림차순

students = [Student('a', 90), Student('b', 80)]
students.sort()
```

> `__lt__`는 `<` 연산 기준을 정의함

---

## **3. 정렬 후 이진 탐색 조합**

* 문제: "정렬된 리스트에서 특정 값을 빠르게 찾기"
* 정렬 후 `bisect` 모듈을 사용

```python
import bisect

arr = [1, 2, 2, 2, 3, 4]
left = bisect.bisect_left(arr, 2)
right = bisect.bisect_right(arr, 2)
print(right - left)  # 값 2의 개수
```

---

## **4. 정렬 기준에 따라 정렬 선택**

| 정렬 알고리즘                          | 평균 시간복잡도                | 특징                 |
| -------------------------------- | ----------------------- | ------------------ |
| `Timsort` (`sort()`, `sorted()`) | O(n log n)              | Python 기본, 빠르고 안정적 |
| Counting Sort                    | O(n + k)                | 숫자 범위 좁을 때 유리      |
| Heap Sort                        | O(n log n)              | 우선순위 큐에 사용         |
| Quick Sort                       | O(n log n) 평균, O(n²) 최악 | 피벗에 따라 성능 좌우       |
| Merge Sort                       | O(n log n)              | 안정 정렬, 메모리 사용 ↑    |

---

## **5. 정렬 + 중복 제거 후 인덱스 압축 (좌표 압축)**

```python
arr = [1000, 2000, 1000, 3000]
sorted_unique = sorted(set(arr))

coord = {num: i for i, num in enumerate(sorted_unique)}
compressed = [coord[num] for num in arr]
# [0, 1, 0, 2]
```

> 많은 범위를 적은 값으로 압축할 때 유용 (예: 10^9 → 0\~N)

---

## **6. lambda key가 복잡해질 경우 함수 분리**

```python
def sort_key(x):
    return (x[1] % 2, -x[0])  # 예: 홀짝 + 값 정렬

arr.sort(key=sort_key)
```

---

## **7. 내림차순 정렬 응용 – `heapq`에서 최대 힙 사용**

* `heapq`는 기본이 **최소 힙**
* 최대 힙처럼 쓰고 싶을 때는 `-값`을 넣기

```python
import heapq

arr = [3, 1, 4]
heap = []
for x in arr:
    heapq.heappush(heap, -x)

print(-heapq.heappop(heap))  # 4
```

---

## **8. 동점자 처리 – 우선순위에 따라 정렬 기준 분기**

```python
arr = [('kim', 90, 1), ('lee', 90, 2), ('park', 80, 3)]

# 점수 내림차순, 점수 같으면 우선순위(세 번째 값) 오름차순
arr.sort(key=lambda x: (-x[1], x[2]))
```

