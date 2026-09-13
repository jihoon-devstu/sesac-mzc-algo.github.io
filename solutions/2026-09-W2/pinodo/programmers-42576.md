---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

collections 라이브러리의 Counter 함수(HashMap상태로 저장)를 이용함.
각 요소의 갯수를 카운트해서 HashMap(dict)로 저장함.
참가자의 카운트 - 완주자의 카운트 = 미완주자의 카운트.
마지막으로 dict를 list로 바꿔주고, 그 안의 string 값을 반환함.

## 풀이

```python
from collections import Counter

def solution(participant, completion):
    return list(Counter(participant) - Counter(completion))[0]

    # Try_1: 시간 초과 (58.3%)
    # for elem in participant:
    #         if (elem not in completion):
    #             return elem
    #         completion.remove(elem)
```

시간 O(n), 공간 O(m)

## 막혔던 부분

처음에는 for elem in participant 순회로 완주자 목록에 있을 시, 완주자 목록에서 하나씩 지움.
답은 맞았지만 시간효율성에서 탈락함.
이후에 Counter 라이브러리를 사용함.
