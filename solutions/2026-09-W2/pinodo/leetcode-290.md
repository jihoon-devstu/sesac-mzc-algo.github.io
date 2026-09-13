---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

두 배열을 동시에 순차적으로 읽고, 이미 hashmap에 있는 value면 res에 문자열로 추가함.
hashmap에 없는 value면 다른 단어에 매핑 되어있는지 여부를 체크 후 res에 문자열로 추가함.

## 풀이

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        s = s.split()
        if (len(pattern) != len(s)): # length check
            return False
        if (len(pattern) == len(s) == 1): # length = 1 => True
            return True

        resDict = {}
        res = ""

        for (ptElem, sElem) in zip(pattern, s):
            if sElem in resDict:
                if ptElem != resDict[sElem]:
                    return False
                res += sElem
            else:
                if ptElem in resDict.values():  # 이미 다른 단어에 매핑된 패턴인지 확인
                    return False
                resDict[sElem] = ptElem
                res += sElem
            # else:
            #     if ptElem in resDict[sElem]:
            #         return False
            #     resDict[sElem] = ptElem
            #     res += sElem
        return True
```

시간복잡도: O(n)

## 막혔던 부분

존재하지 않는 키를 참조하려 해서 계속 오류가 났음