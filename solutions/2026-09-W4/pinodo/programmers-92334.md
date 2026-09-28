---
status: done
language: python
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명
- 유저 리스트, 리포트("신고자 피신고자"형식의 문자열), 정지 기준이 되는 신고 횟수 순으로 파라미터 구성
- 내가 신고한 유저 중, 정지 신고 횟수를 넘어서 정지가 된 유저의 숫자를 리스트로 반환함
- 중복 신고는 무시됨

## 접근
- uid-index 를 해시맵으로 저장
- 중복된 신고 제거 후 reported_set에 저장(Set)
- 각각 다른 신고자에게 신고당한 횟수를 count에 저장
- 정지 기준 횟수 넘으면 카운트


## 풀이

```python
# AI
def solution(id_list, report, k):
  # id_list의 유저-id(k-v)를 저장 
  idx_of = {uid: i for i, uid in enumerate(id_list)}
  answer = [0] * len(id_list)

  reported_set = set()
  for r in report:
      reporter, reported = r.split()
      reported_set.add((reporter, reported))  # 같은 쌍은 자동으로 1회 처리

  count = {}  # 신고당한 횟수
  for _, reported in reported_set:
      count[reported] = count.get(reported, 0) + 1

  for reporter, reported in reported_set:
      if count[reported] >= k:
          answer[idx_of[reporter]] += 1

  return answer

# Try_1: 문제 이해 잘못함
# def solution(id_list, report, k):
#     reported_list = set()
#     answer = [0] * (len(id_list))
#     for i in range(len(report)):
#         reporter, reported = report[i].split()
#         if (reported_list == None):
#             reported_list.add((reporter, reported))
#             idx = id_list.index(reporter)
#             answer[idx] = 1
#         if ((reporter, reported) not in reported_list):
#             reported_list.add((reporter, reported))
#             idx = id_list.index(reporter)
#             answer[idx] += 1
#         else:
            
#     return answer
```

시간복잡도: O(n)

## 막혔던 부분
