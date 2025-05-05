
## 딕셔너리(Dictionary) 다룰 때 알아두면 좋은 문법

## 1. 딕셔너리 생성과 기본 조작

```python
d = {'a': 1, 'b': 2}
d = dict(a=1, b=2)

d['c'] = 3          # 추가/수정
del d['b']          # 삭제
```

## 2. 값 조회와 예외 처리

```python
value = d['a']           # KeyError 발생 가능
value = d.get('x')       # None 반환
value = d.get('x', 0)    # 기본값 지정
```

## 3. 반복문을 통한 순회

```python
for key in d:
    print(key, d[key])

for key, val in d.items():
    print(key, val)

for val in d.values():
    print(val)
```

## 4. 주요 메서드 정리

| 메서드           | 설명            |
| ------------- | ------------- |
| d.keys()      | 키 목록          |
| d.values()    | 값 목록          |
| d.items()     | (키, 값) 쌍 목록   |
| d.get(k, def) | 키 없을 때 기본값 반환 |
| d.pop(k)      | 키 제거 후 값 반환   |
| d.clear()     | 딕셔너리 비우기      |
| k in d        | 키 존재 여부 확인    |

## 5. 딕셔너리 컴프리헨션

```python
squared = {x: x**2 for x in range(5)}
```

## 6. defaultdict 기본값 설정

```python
from collections import defaultdict

d = defaultdict(int)
d['apple'] += 1

d = defaultdict(list)
d['fruit'].append('apple')
```

## 7. Counter로 등장 횟수 세기

```python
from collections import Counter

arr = ['a', 'b', 'a', 'c']
count = Counter(arr)
```

## 8. 딕셔너리 정렬

```python
sorted_items = sorted(d.items())  # 키 기준
sorted_by_val = sorted(d.items(), key=lambda x: x[1])  # 값 기준
```

## 9. 2차원 딕셔너리 예시

```python
from collections import defaultdict

graph = defaultdict(dict)
graph['A']['B'] = 5
```

## 10. 복합 키 (튜플)

```python
d = {}
d[(1, 2)] = 'value'
```
