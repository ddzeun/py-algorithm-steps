
## 정렬 관련 python 코테 문법

## **1. 기본 정렬 (sort vs sorted)**

```python
arr = [3, 1, 4, 2]

arr.sort()         # in-place 정렬 → [1, 2, 3, 4]
arr.sort(reverse=True)  # 내림차순

new_arr = sorted(arr)  # 원본은 유지, 새 리스트 반환
```

| 함수         | 특징       | 반환      |
| ---------- | -------- | ------- |
| `sort()`   | 제자리 정렬   | `None`  |
| `sorted()` | 새 리스트 반환 | 정렬된 리스트 |

---

## **2. key=lambda를 이용한 커스텀 정렬**

```python
words = ['apple', 'banana', 'kiwi', 'avocado']

# 문자열 길이순 정렬
words.sort(key=lambda x: len(x))  # ['kiwi', 'apple', 'banana', 'avocado']
```

`key=lambda`로 정렬 기준을 직접 지정

---

## **3. 튜플 & 리스트 정렬**

```python
arr = [(3, 'c'), (1, 'a'), (2, 'b')]

# 첫 번째 원소 기준 정렬
arr.sort()  # [(1, 'a'), (2, 'b'), (3, 'c')]

# 두 번째 원소 기준 정렬
arr.sort(key=lambda x: x[1])  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

---

## **4. 다중 조건 정렬**

```python
students = [
    ('alice', 90),
    ('bob', 85),
    ('carol', 90),
    ('dave', 80)
]

# 점수 내림차순, 이름 오름차순
students.sort(key=lambda x: (-x[1], x[0]))
# [('alice', 90), ('carol', 90), ('bob', 85), ('dave', 80)]
```

---

## **5. 숫자 문자열 정렬**

```python
nums = ['10', '2', '30']

# 문자열 기준 (사전순)
sorted(nums)  # ['10', '2', '30']

# 숫자 기준 정렬
sorted(nums, key=int)  # ['2', '10', '30']
```

---

## **6. 정렬 기준이 복잡할 땐 함수로 분리**

```python
def custom_key(x):
    return (x[1], -x[0])  # 두 번째 오름차순, 첫 번째 내림차순

arr = [(1, 2), (2, 2), (3, 1)]
arr.sort(key=custom_key)
```

---

## **7. 정렬 응용 – 순위 매기기**

```python
scores = [80, 90, 75]
sorted_scores = sorted(scores, reverse=True)

for s in scores:
    rank = sorted_scores.index(s) + 1
    print(f"{s}점: {rank}등")
```

> 동점 처리, 빠른 순위 계산이 필요하면 `dict` 활용 or `enumerate` 조합이 좋음

---

## **8. 정렬 응용 – 좌표 정렬 문제 (백준 자주 출제)**

```python
points = [(1, 2), (2, 2), (3, 1)]

# y 오름차순 → 같으면 x 오름차순
points.sort(key=lambda x: (x[1], x[0]))
```

---

## **9. 정렬 응용 – 문자열 정렬 문제**

```python
words = ['ab', 'abc', 'a', 'abcd']

# 길이 짧은 순, 같으면 사전순
words.sort(key=lambda x: (len(x), x))
```

---

## **10. 리스트 압축 + 정렬**

```python
arr = list(set(arr))  # 중복 제거
arr.sort()
```