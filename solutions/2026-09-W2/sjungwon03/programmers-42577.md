---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

### 1차 풀이
- 해시맵으로 접근할 방법이 생각나지 않아서 완전탐색 방식으로 풀었습니다.
- 배열을 순회하면서 다른 요소에 해당 문자가 포함되는지를 검사
- O(N^2)
-> `시간 초과`

### 2차 풀이
- 모든 문자열을 HashSet에 저장해두고, 문자열 배열을 돌면서 현재 문자열의 SubString이 HashSet에 있는지 검토하는 식으로 개선하는 방법을 떠올렸습니다.
- 이 경우 문자열 배열을 2번 순회하므로 O(2 * N) -> O(N) 만에 풀이가 가능합니다.

## 풀이

### 1차 풀이
```cpp
#include <string>
#include <vector>

using namespace std;

bool solution(vector<string> phone_book) {
    bool answer = true;
    
    for (int i = 0; i < phone_book.size(); i++) {
        string cur = phone_book[i];

        for (int j = 0; j < phone_book.size(); j++) {
            if (i == j) {
                continue;
            }

            string cmp = phone_book[j];

            if (cur.size() < cmp.size()) {
                bool isSame = (cmp.substr(0, cur.size()) == cur);

                if (isSame) {
                    return false;
                }
            } else {
                bool isSame = (cur.substr(0, cmp.size()) == cmp);

                if (isSame) {
                    return false;
                }
            }
        }
    }
    
    return answer;
}
```

- 결과
```
채점을 시작합니다.
정확성  테스트
테스트 1 〉	통과 (0.00ms, 4.82MB)
테스트 2 〉	통과 (0.00ms, 4.7MB)
테스트 3 〉	통과 (0.01ms, 4.67MB)
테스트 4 〉	통과 (0.01ms, 4.7MB)
테스트 5 〉	통과 (0.01ms, 4.7MB)
테스트 6 〉	통과 (0.01ms, 4.92MB)
테스트 7 〉	통과 (0.01ms, 4.82MB)
테스트 8 〉	통과 (0.00ms, 4.63MB)
테스트 9 〉	통과 (0.01ms, 4.79MB)
테스트 10 〉	통과 (0.00ms, 4.76MB)
테스트 11 〉	통과 (0.00ms, 4.67MB)
테스트 12 〉	통과 (0.00ms, 4.7MB)
테스트 13 〉	통과 (0.01ms, 4.7MB)
테스트 14 〉	통과 (13.72ms, 5.07MB)
테스트 15 〉	통과 (12.06ms, 4.95MB)
테스트 16 〉	통과 (76.54ms, 4.79MB)
테스트 17 〉	통과 (112.27ms, 4.82MB)
테스트 18 〉	통과 (161.61ms, 4.63MB)
테스트 19 〉	통과 (75.04ms, 4.7MB)
테스트 20 〉	통과 (120.62ms, 4.92MB)
효율성  테스트
테스트 1 〉	통과 (0.30ms, 4.57MB)
테스트 2 〉	통과 (0.31ms, 4.57MB)
테스트 3 〉	실패 (시간 초과)
테스트 4 〉	실패 (시간 초과)
채점 결과
정확성: 83.3
효율성: 8.3
합계: 91.7 / 100.0
```
- 이중반복문 시간복잡도 O(N^2), 공간복잡도 O(L) (cur, cmp, substr())

### 2차 풀이
```cpp
#include <string>
#include <vector>
#include <unordered_set>

using namespace std;

bool solution(vector<string> phone_book) {
    unordered_set<string> str;

    for (int i = 0; i < phone_book.size(); i++) {
        str.insert(phone_book[i]);
    }

    for (int i = 0; i < phone_book.size(); i++) {
        string cur = phone_book[i];

        for (int j = 1; j < cur.size(); j++) {
            string sub = cur.substr(0, j);

            if (str.find(sub) != str.end()) {
                return false;
            }
        }
    }

    return true;
}
```
- HashSet에 숫자를 우선 넣어주고 각 문자열의 substr이 Set에 존재하는지 검사했습니다.
- 이 경우 문자열 최대 길이는 20, 배열을 한번 순회하므로 시간복잡도 O(N)만에 실행이 가능합니다.
- 공간복잡도의 경우 모든 문자열을 Set에 저장하므로 O(N)이 됩니다.

### GPT 해설
요약하면 이렇게입니다.

* 1차 풀이 시간복잡도

  * 엄밀하게는 `O(N² × L)`
  * 전화번호 길이 `L <= 20`을 상수로 보면 `O(N²)`

* 1차 풀이 공간복잡도

  * 보조 공간만 보면 `O(L)`
  * 함수 인자 `phone_book` 복사까지 포함하면 `O(N × L)`

* 2차 풀이 시간복잡도

  * `substr()` 생성 + 문자열 해시/비교 비용까지 고려하면 `O(N × L²)`
  * `L <= 20`이므로 이 문제에서는 사실상 `O(N)`

* 2차 풀이 공간복잡도

  * `unordered_set`에 모든 문자열을 저장하므로 `O(N × L)`
  * `L <= 20`을 상수로 보면 `O(N)`

* `unordered_set` 탐색은 정확히는 평균 `O(1)`

* 문자열은 `"포함"`이 아니라 `"접두어인지 검사"`라고 표현하는 게 정확함


## 막혔던 부분

- 배열을 HashMap 혹은 HashSet 형태로 변경하면 같은 값을 찾는데 O(1)만에 가능함을 떠올리지 못해 한번에 풀지 못했습니다.