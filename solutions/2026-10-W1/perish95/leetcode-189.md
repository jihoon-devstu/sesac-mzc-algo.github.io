---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명

- 주어진 배열 `nums`에서 `k`만큼 맨 뒤의 수를 맨 앞으로 보내면 되는 문제이다.(시계 방향으로 회전)

## 접근

- deque를 사용해서 뒤에서 수를 뽑아서 앞에 넣어주었다.

## 풀이

```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        deque<int> dq;

        for(auto n : nums){
            dq.push_back(n);
        }

        for(int i=0;i<k;i++){
            dq.push_front(dq.back());
            dq.pop_back();
        }

        for(int i=0;i<nums.size();i++){
            nums[i] = dq.front();
            dq.pop_front();
        }
    }
};

```

시간복잡도 O(n)
소요시간: 약 10분

## 막혔던 부분
