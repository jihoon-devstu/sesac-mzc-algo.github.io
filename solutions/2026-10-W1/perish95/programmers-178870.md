---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명

- 오름차순의 배열 `sequence`와 부분 수열의 합을 나타내는 정수 `k`를 매개변수로 준다.
- 이 때, 두 인덱스를 사이의 포함한 부분 수열의 합이 `k`와 같을 경우 부분 수열의 시작과 끝의 인덱스를 반환한다.
- 여러 개의 답이 있을 경우 부분 수열이 짧은 것이 우선 순위이며, 길이가 같은 경우 시작 인덱스가 작은 수열을 반환한다.

## 접근

- 투 포인터로 접근하되 포인터의 위치를 둘 다 0으로 한다.
- `k`보다 합이 작을 경우 `right`를 증가시키고, 합이 작을 경우는 `left`를 증가시킨다.
- `k`의 범위가 커서 `long long`으로 선언

## 풀이

```C++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> sequence, int k) {
    int left = 0, right = 0;
    int sLeft = 0, sRight = sequence.size() - 1;
    long long sum = sequence[0];

    while (right < sequence.size()) {
        if (sum == k) {
            if (right - left < sRight - sLeft) {
                sLeft = left;
                sRight = right;
            }
        }

        if (sum < k) {
            right++;
            if (right < sequence.size()) {
                sum += sequence[right];
            }
        }
        else {
            sum -= sequence[left];
            left++;
        }
    }

    return {sLeft, sRight};
}

```

시간복잡도O(n)
소요시간: 약 30분

## 막혔던 부분

while 조건문 설정을 너무 어렵게 생각했는데, 심플하게 접근하는 것이 맞았다.
