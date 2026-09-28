---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명
- 주어진 리스트 안의 정수를 조합해 문자열형식으로 붙여 가장 큰 숫자 만들기


## 접근
- 각 원소의 맨 앞자리수를 비교해서 정렬
- 앞자리수가 같을 경우, 두개의 원소를 앞뒤로 붙여서 더 큰 숫자가 나오도록 배치
- 구현 잘 모르겠어서 AI 이용

## 풀이

```python
# AI
from functools import cmp_to_key

def solution(numbers):
    strs = [str(n) for n in numbers]
    strs.sort(key=cmp_to_key(lambda a, b: (1 if a + b < b + a else -1)))
    answer = ''.join(strs)
    return '0' if answer[0] == '0' else answer

# 핵심은 a + b와 b + a를 만들어 비교하는 부분이에요.
# 예를 들어 a="3", b="30"이면 "330"과 "303"을 비교해서 "330"이 크니까 3이 앞으로 가요.
# 비교 함수는 a가 앞에 와야 하면 음수, 뒤에 와야 하면 양수를 반환하는 규칙이라 각각 -1과 1을 돌려줬어요.

```

시간복잡도: O(n)

## 막혔던 부분
