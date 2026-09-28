---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명
- h-index 값 구하기
- 주어진 리스트 안에서 한 원소(h)가 h번 이상 반복되는 값(h) 구하기


## 접근
- 리스트를 정렬함
- 정렬된 리스트 순회하면서 해당 값보다 남은 원소 갯수가 크거나 같으면 값을 반환

## 풀이

```python
def solution(citations):
    citations.sort()
    n = len(citations)
    for i in range(n):
        if citations[i] >= n - i:
            return n - i
    return 0

# Try_1
# def solution(citations):
#     citations.sort()
#     for i in range(len(citations)):
#         if (len(citations) - citations[i] + 1 == citations[i]):
#             return citations[i]
#     return 0
```

시간복잡도: O(n)

## 막혔던 부분
