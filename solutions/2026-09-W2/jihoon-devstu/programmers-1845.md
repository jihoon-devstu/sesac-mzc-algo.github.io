---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

1. 중복없이 포켓몬 종류에 대한 Hashmap을 만들기.
2. Hashmap의 사이즈와 nums의 2분의1사이즈를 비교하여 , Hashmap의 사이즈가 더 큰경우 , Hashmap의 사이즈 반환 , 반대는 nums의2분의1사이즈 반환

## 풀이

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int solution(int[] nums) {
        
        int halfnums = (nums.length/2);
        
        Map<Integer,Integer> pcount = new HashMap<>();
        
        for(int c : nums){
            pcount.put(c,1);
        }
        
        int psize = pcount.size();
        
        int answer = psize > halfnums ? halfnums : psize;
        return answer;
    }
}
```

시간 : O(N) , 공간 : O(N)

## 막혔던 부분

1. 배열의 사이즈와 hashmap의 사이즈 추출 함수 -> .length 와 .size()