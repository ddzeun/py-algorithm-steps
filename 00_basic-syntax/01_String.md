
## 문자열을 다룰 때 알아두면 좋은 문법


## 1. **문자열 입력**
.strip() 붙여서 개행 제거하기

```python
s = input().strip()
```

---

## 2. **문자열 양쪽/왼쪽/오른쪽 공백 제거**
입력받은 문자열 다룰 때 필수

```python
s = "  hello  "

print(s.strip())   # 양쪽 공백 제거 → "hello"
print(s.lstrip())  # 왼쪽 공백 제거 → "hello  "
print(s.rstrip())  # 오른쪽 공백 제거 → "  hello"
```

## 3. **문자열 슬라이싱**
문자열을 원하는 범위로 뽑아내기

```python
s = "Hello"
s[0]      # 'H'
s[-1]     # 'o'
s[1:4]    # 'ell'
s[::-1]   # 문자열 뒤집기: 'olleH'
```

---

## 4. **문자/문자열 비교**

```python
if s == "Hello":
    ...
if s.lower() == "hello":  # 대소문자 무시하고 비교
    ...
```

---

## 5. **부분 문자열 찾기 (Substring 찾기)**
문자열 안에 "특정 문자열"이 포함되어 있는지 검사할 때

```python
s = "hello world"

# 포함 여부 확인
if "world" in s:
    print("있다!")

# 위치 찾기
print(s.find("world"))  # 6 (index 반환), 없으면 -1
print(s.index("world")) # 6 (index 반환), 없으면 오류
```

> `in`은 True/False, `find()`는 위치를 

---

## 6. **아스키코드 다루기 (ord, chr)**

```python
ord('A')    # 65
chr(97)     # 'a'
```

> 문자 ↔ 숫자 변환은 **카운팅 배열 만들 때**, 또는 **사전 순 정렬**, **암호화 문제** 등에서 사용

---

## 7. **문자열 반복 / 결합**

```python
s = "abc"
print(s * 3)           # 'abcabcabc'
print("a" + "b")       # 'ab'
```

---


## 8 **문자열 쪼개기 & 합치기**
문자열을 쪼개서(split) 리스트로 만들고, 다시 문자열로 합치기(join)<br>
**join은 리스트 요소가 전부 문자열 타입이어야 함.**

```python
# 공백 기준으로 split
s1 = "a b   c d"
print(s.split())  # ['a', 'b', 'c', 'd']

s2 = "apple,banana,grape"

fruits = s2.split(",")
print(fruits)  # ['apple', 'banana', 'grape']

# 다시 합치기
new_s = ",".join(fruits)
print(new_s)  # "apple,banana,grape"
```

> 많이 쓰임. split과 join은 세트

---

## 9. **대소문자 변환**
문자열을 대문자/소문자로 통일해서 비교하거나 다룰 때

```python
s = "BaNaNa"

print(s.upper())  # "BANANA"
print(s.lower())  # "banana"
print(s.capitalize())  # "Banana" (맨 앞글자만 대문자)
```

---

## 10. **문자 판별 (isalpha, isdigit, isalnum)**
문자열이 어떤 종류인지 검사할 때!

```python
s1 = "abc"
s2 = "123"
s3 = "abc123"

print(s1.isalpha())  # True (문자만)
print(s2.isdigit())  # True (숫자만)
print(s3.isalnum())  # True (문자 + 숫자)
```

---


## 11. *문자열 정렬 (정렬은 리스트로 바꿔야 가능)*

```python
s = "cab"
sorted_s = sorted(s)       # ['a', 'b', 'c']
"".join(sorted_s)          # 'abc'
```

---

## 12. **문자열 뒤집기**
문자열을 거꾸로 만드는 테크닉

```python
s = "hello"
reversed_s = s[::-1]
print(reversed_s)  # "olleh"
```

> `[::-1]` 은 꼭 기억하기

---

## 13. **문자열 처리 함수들**

```python
s = "Python is fun"

s.upper()        # 'PYTHON IS FUN'
s.lower()        # 'python is fun'
s.count("o")     # 2
s.find("is")     # 7 (못 찾으면 -1)
s.index("is")    # 7 (못 찾으면 에러)
s.replace("fun", "awesome")  # 'Python is awesome'
```

---

## 14. **Counter (문자 개수 세기)**
여러 번 등장하는 문자 개수 세고 싶을 때

```python
from collections import Counter

s = "banana"
count = Counter(s)
print(count)  # Counter({'a': 3, 'n': 2, 'b': 1})

# 가장 많이 등장한 문자
print(count.most_common(1))  # [('a', 3)]
```

Counter로 정렬도 할 수 있다.
```python
from collections import Counter

s = "banana"
count = Counter(s)

# 등장 횟수 내림차순 정렬
for char, cnt in count.most_common():
    print(char, cnt)

```

---

## 15. **정규표현식 (regex) — 심화**
아주 복잡한 패턴 찾을 때

```python
import re

s = "abc123def456"

# 숫자만 골라내기
numbers = re.findall(r'\d+', s)
print(numbers)  # ['123', '456']

# 알파벳만 골라내기
letters = re.findall(r'[a-zA-Z]+', s)
print(letters)  # ['abc', 'def']
```

---


## 16. **문자열은 불변(immutable)**

```python
s = "hello"
s[0] = 'H'   # 에러 발생

# 수정하려면 리스트로 변환 후 작업
s_list = list(s)
s_list[0] = 'H'
s = ''.join(s_list)
```
