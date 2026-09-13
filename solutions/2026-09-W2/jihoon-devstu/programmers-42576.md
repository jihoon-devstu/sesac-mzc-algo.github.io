---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

1. 참가자 명단을 HashMap으로 생성하여 value에 동명이인 여부를 체크
2. 완주자 명단을 순회하며 value 에 -1
3. value가 1인 key값 추출하여 제출

## 풀이

```java
import java.util.List;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        
        Map<String,Integer> pcount = new HashMap<>();
        
        for(String s : participant) {
            pcount.put(s,pcount.getOrDefault(s,0)+1);
        }
        
        for(String s : completion) {
            pcount.put(s,pcount.getOrDefault(s,0)-1);
        }
        
        List<String> keyList = new ArrayList<>(pcount.keySet());
        
        for(int i = 0; i<keyList.size() ; i++){
            if(pcount.get(keyList.get(i)) == 1){
                answer = keyList.get(i);
            }
        }
        
        
        return answer;
    }
}
```

시간 : O(N) , 공간 : O(N)

소요시간: 약 40분

## 막혔던 부분

1. 동명이인을 구분하기 위해 key값과 value 값을 둘 다 활용해야 했던 점
2. keyList를 ArrayList로 만들어 다시 값을 각각 입력하며 순회시킨다음 추출해야 했던 점