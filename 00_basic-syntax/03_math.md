## 수학 관련 알아두면 좋은 문법

---

## 1. **기본 연산**
```python
a + b       # 덧셈
a - b       # 뺄셈
a * b       # 곱셈
a / b       # 나눗셈 (항상 float 반환)
a // b      # 몫
a % b       # 나머지
a ** b      # 거듭제곱
```

---

## 2. **절댓값, 최댓값, 최솟값**
```python
abs(-5)         # 5
max(1, 5, 3)    # 5
min(1, 5, 3)    # 1
```

---

## 3. **수학 함수 모음**

```python
import math         # 모듈 import 확인

math.sqrt(16)       # 제곱근 4.0
math.pow(2, 3)      # 2^3 = 8.0
math.factorial(5)   # 5! = 120
math.gcd(12, 18)    # 최대공약수 6
```

---

## 4. **소수 판별**

```python
def is_prime(x):
    if x < 2:
        return False
    for i in range(2, int(x**0.5)+1):
        if x % i == 0:
            return False
    return True
```
> **2부터 √x까지**만 확인

---

## 5. **에라토스테네스의 체 (Prime Sieve)**

```python
def sieve(n):
    primes = [True] * (n+1)
    primes[0] = primes[1] = False
    for i in range(2, int(n**0.5)+1):
        if primes[i]:
            for j in range(i*i, n+1, i):
                primes[j] = False
    return primes
```
> **모든 소수 한 번에 찾는 최적화 방법**

---

## 6. **약수 구하기**

```python
def get_divisors(n):
    divisors = []
    for i in range(1, int(n**0.5)+1):
        if n % i == 0:
            divisors.append(i)
            if i != n // i:
                divisors.append(n//i)
    return divisors
```
> **한쪽만 돌리고, 짝이 되는 약수 같이 저장**

---

## 7. **최소공배수 구하기**

```python
import math

def lcm(a, b):
    return a * b // math.gcd(a, b)
```
> **GCD(최대공약수) 활용**

---

## 8. **거듭제곱 빠르게 계산**

```python
def power(x, n):
    result = 1
    while n:
        if n % 2:
            result *= x
        x *= x
        n //= 2
    return result
```
> 시간복잡도 **O(log n)** 로 거듭제곱 계산  

---

## 9. **나머지 연산 심화 (MOD 연산)**

> 큰 수를 다룰 때 중간 결과에 **mod 연산을 끼워넣어** 오버플로우 방지

```python
MOD = 10**9 + 7

a = (a + b) % MOD
a = (a - b) % MOD
a = (a * b) % MOD
a = (a * pow(b, MOD-2, MOD)) % MOD      # b의 역원으로 나누기
```

> (파이썬 pow는 pow(b, MOD-2, MOD)로 역원 계산도 가능)

---


## 10. **순열(Permutation)과 조합(Combination)**

```python
import math

# 순열: nPr = n! / (n-r)!
def permutation(n, r):
    return math.factorial(n) // math.factorial(n - r)

# 조합: nCr = n! / (r! * (n-r)!)
def combination(n, r):
    return math.factorial(n) // (math.factorial(r) * math.factorial(n - r))
```

> - **순열(permutation):** 순서 O  
> - **조합(combination):** 순서 X

---

## 11. **조합/순열 빠르게 구하기 (math 모듈)**

```python
import math

math.comb(5, 2)     # 5C2 = 10
math.perm(5, 2)     # 5P2 = 20
```

> **파이썬 3.8 이상**부터 math 모듈에 `comb`, `perm` 추가됨

---

## 12. **이항 계수**

> `nCr`를 빠르게 구하는 공식

```python
def binomial(n, r):
    result = 1
    for i in range(1, r+1):
        result = result * (n - i + 1) // i
    return result
```
> 팩토리얼 없이도 계산 가능 (오버플로 방지에 좋음)

---

## 13. **모듈러 곱셈/나눗셈 공식 (MOD)**

> (a × b) % m = ((a % m) × (b % m)) % m

> (a ÷ b) % m = (a × b의 모듈러 역원) % m

---

## 14. **모듈러 역원 (Modular Inverse)**

> 페르마 소정리(Fermat’s Little Theorem) 활용

- 소수 p에 대해:  
  b^(p-1) ≡ 1 (mod p)

- 따라서,  
  b^(p-2) ≡ b^(-1) (mod p)

```python
MOD = 10**9 + 7
inverse_b = pow(b, MOD-2, MOD)
```
> **나눗셈이 필요한 문제에서 많이 등장**

---

## 15. **등차수열, 등비수열 합 공식**

- 등차수열 합: `n * (첫항 + 마지막항) // 2`
- 등비수열 합: 첫항 × (1 - rⁿ) / (1 - r)

```python
# 등차수열 합 예시
n = 100
a1 = 1
an = 100
sum_arith = n * (a1 + an) // 2
```

---

## 16. **최대공약수 배열 (GCD of array)**

```python
import math

def gcd_list(arr):
    result = arr[0]
    for num in arr[1:]:
        result = math.gcd(result, num)
    return result
```
> 리스트 전체의 GCD를 구할 때

---

## 17. **최대/최소 쌍 합 구하기 (Two Pointer)**

> **정렬 후 양끝에서 투포인터로 합 구하는 테크닉**

```python
arr.sort()
left, right = 0, len(arr)-1
while left < right:
    s = arr[left] + arr[right]
    if s == target:
        # 정답 처리
        left += 1
        right -= 1
    elif s < target:
        left += 1
    else:
        right -= 1
```

---

## 18. **합동(modulo) 공식 정리**

- (a + b) mod m = (a mod m + b mod m) mod m  
- (a - b) mod m = (a mod m - b mod m + m) mod m  
- (a × b) mod m = (a mod m × b mod m) mod m  
- (a ÷ b) mod m = (a mod m × b^(m-2) mod m) mod m (**b가 소수일 때만**)

> 문제에 "나머지 구해라"라는 말 나오면 바로 떠올리기

---

## 19. **빠른 팩토리얼 및 nCr % MOD 계산**

```python
MOD = 10**9 + 7
MAX = 10**6

# 1. 팩토리얼과 역팩토리얼 미리 구해놓기
fact = [1] * (MAX+1)
inv_fact = [1] * (MAX+1)

for i in range(1, MAX+1):
    fact[i] = (fact[i-1] * i) % MOD

inv_fact[MAX] = pow(fact[MAX], MOD-2, MOD)
for i in range(MAX-1, 0, -1):
    inv_fact[i] = (inv_fact[i+1] * (i+1)) % MOD

# 2. nCr % MOD 구하기
def nCr(n, r):
    if r < 0 or r > n:
        return 0
    return fact[n] * inv_fact[r] % MOD * inv_fact[n-r] % MOD
```
> **nCr % MOD 문제는 미리 계산한 테이블을 이용해 O(1)로 구함**
