---
status: done
language: java
---

## 접근

1. LRU(Least Recently Used)는 캐시가 꽉 찼을 때 가장 오랫동안 쓰지 않은 항목을 버리는 방식이다.
2. 캐시를 `오래된 순 → 최근 순`으로 담는 List로 관리한다.
3. 도시 이름은 대소문자를 구분하지 않으므로 `toLowerCase()`로 키를 통일한다.
4. cache hit: 리스트에서 제거한 뒤 맨 뒤에 다시 넣어 가장 최근으로 갱신한다. (+1)
5. cache miss: 캐시가 꽉 찼으면 맨 앞(가장 오래된 항목)을 제거하고 맨 뒤에 넣는다. (+5)
6. `cacheSize`가 0이면 아무것도 저장할 수 없으므로 전부 miss로 처리한다.

## 풀이

```java
import java.util.*;
class Solution {
    public int solution(int cacheSize, String[] cities) {
        int time =0;
        if (cacheSize == 0) return cities.length * 5;
        List<String> cache = new ArrayList<>();
        for (String city : cities) {
            String key = city.toLowerCase();
            // 캐시 존재하면 제거
            if (cache.remove(key)) {
                time +=1;
            } else {
                time +=5;
                // 존재하지 않는데 캐시 사이즈가 차있으면 제일 오래된 캐시 제거
                if (cache.size() == cacheSize) {
                    cache.remove(0);
                }
            }
            
            // 캐시 추가
            cache.add(key);
        }
        return time;
    }
}
```

시간 O(N × cacheSize), 공간 O(cacheSize)

## 막혔던 부분

1. LRU 알고리즘이 무엇인지 파악하는 부분
2. LRU를 구현할 때 HashMap, List, Queue 중 어떤 자료구조를 써야 할지 고민했던 부분
