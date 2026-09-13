---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

단순 구현 문제로 짝수번에는 `수` 홀수번에는 `박`을 문자열에 추가하도록 구현했습니다. 

## 풀이

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(int n) {
    string answer = "";
    
    for(int i = 0; i < n; i++){
        if(i%2 == 0){
            answer += "수";
        }else {
            answer += "박";
        }
    }
    
    return answer;
}
```

시간 복잡도는 문자열 길이를 반복하므로 O(n)
공간 복잡도는 answer 길이만큼 사용하므로 O(n)

## 막혔던 부분

