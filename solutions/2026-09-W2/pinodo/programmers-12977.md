---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

combinations 라이브러리를 통해 세 숫자의 조합을 리스트에 넣고, 각 조합의 합을 구함.
별도의 소수 판별 메서드를 통해 소수인지 판별하고, 소수가 맞으면 res값을 하나 올림.

## 풀이

```python
from itertools import combinations

def solution(nums) -> int:
    res = 0
    outputs = list(combinations(nums, 3))
    for i in range(len(outputs)):
        sums = sum(outputs[i])
        print(sums, isPrimeNum(sums))
        if (isPrimeNum(sums)):
            res += 1
    return res

def isPrimeNum(num) -> bool:
    if (num == 1): return False
    if (num == 2): return True
    for i in range(3, num):
        if (num % i == 0):
            return False
    return True
```

시간복잡도: O(n)

## 막혔던 부분

소수를 구하는 메서드 구현이 생각이 안남. 3부터 num-1까지의 모든 수를 순회