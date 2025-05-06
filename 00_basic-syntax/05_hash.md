
## 해시(Hash) 자료구조 정리

---

## 해시(Hash)란?

**해시는 데이터를 고정된 크기의 값으로 '매핑(mapping)'하는 방식**

> 어떤 값을 입력하면 → 일정한 규칙에 따라 → 고유한 숫자(또는 문자열)로 변환하는 것

이걸 수행하는 함수가 **해시 함수(hash function)** 이고, <br>
이 결과값을 **해시값(hash value)**

* 값을 **빠르게 찾기 위해서** (탐색 속도 향상)
* 데이터를 **고유하게 식별하기 위해서**
* 키-값 구조로 **데이터를 저장하기 위해서** (ex. 딕셔너리)

---

## 예시: 전화번호부 찾기

만약 리스트로 사람 이름을 찾아야 하면 일일이 순회해야 해서 시간 복잡도는 `O(n)`

하지만 딕셔너리는 내부적으로 **이름을 해시값으로 바꿔서 빠르게 주소(인덱스)를 찾아감**. → `O(1)`에 가까움.

```python
phone_book = {'Alice': '010-1234', 'Bob': '010-5678'}
print(phone_book['Alice'])  # 해시값으로 내부적으로 빠르게 찾음
```

| 개념     | 설명                                       |
| ------ | ---------------------------------------- |
| 해시     | 값을 고정된 크기의 고유 값으로 매핑하는 방식                |
| 해시 함수  | 데이터를 해시값으로 바꿔주는 함수                       |
| 해시 테이블 | 해시값을 인덱스로 사용하는 데이터 저장 구조 (ex. 딕셔너리, set) |
| 장점     | 빠른 탐색 속도 (`O(1)` 기대), 키 중복 없음            |
| 단점     | 해시 충돌 가능성, 순서 없음                         |

---

## 1. 기본 사용법 (딕셔너리)

```python
# 생성 및 추가
my_dict = {}
my_dict['apple'] = 3

# 조회
print(my_dict['apple'])       # 존재하면 값 출력
print(my_dict.get('banana'))  # 존재하지 않으면 None 반환

# 존재 여부
if 'apple' in my_dict:
    ...

# 삭제
del my_dict['apple']
```

---

## 2. 딕셔너리 순회

```python
for key in my_dict:
    print(key, my_dict[key])

for key, value in my_dict.items():
    print(key, value)
```

---

## 3. 기본값 처리 (defaultdict)

```python
from collections import defaultdict

# 기본값이 0인 정수형 딕셔너리
count = defaultdict(int)
count['apple'] += 1
```

---

## 4. 등장 횟수 세기 (Counter)

```python
from collections import Counter

words = ['a', 'b', 'a', 'c']
counter = Counter(words)

print(counter['a'])       # 2
print(counter.most_common(1))  # [('a', 2)]
```

---

## 5. 해시셋 (set)

```python
s = set()

s.add(1)
s.remove(1)
s.discard(2)  # 존재하지 않아도 에러 X

# 존재 확인
if 3 in s:
    ...

# 중복 제거
arr = [1, 1, 2, 3]
unique = list(set(arr))
```

---

## 6. 두 집합 연산

```python
a = {1, 2, 3}
b = {3, 4, 5}

a & b  # 교집합 {3}
a | b  # 합집합 {1,2,3,4,5}
a - b  # 차집합 {1,2}
```

---

## 7. 딕셔너리 정렬

```python
# 키 기준 정렬
sorted_dict = dict(sorted(my_dict.items()))

# 값 기준 정렬
sorted_items = sorted(my_dict.items(), key=lambda x: x[1], reverse=True)
```

---

## 8. 해시 충돌 방지 키 구성

```python
# 예: 2차원 좌표를 키로 사용
visited = {}
x, y = 2, 3
visited[(x, y)] = True
```

---

## 9. 키 존재 여부 체크 없이 추가

```python
# 방법 1
if key not in d:
    d[key] = 0
d[key] += 1

# 방법 2 (defaultdict 사용)
from collections import defaultdict
d = defaultdict(int)
d[key] += 1
```

---

## 10. 문자열 아나그램 판별

```python
from collections import Counter

def is_anagram(a, b):
    return Counter(a) == Counter(b)
```
