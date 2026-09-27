---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

- 숫자 오름차순 정렬
- 현재 citations[i](인용 횟수)가 남은 배열 원소의 수보다 크면 (해당 숫자보다 뒤에 있는 숫자는 더 많이 인용되었음) 남은 배열의 원소수를 h로 설정

## 풀이

```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);

        for (int i = 0; i < citations.length; i++) {
            int h = citations.length - i;

            if (citations[i] >= h) {
                return h;
            }
        }

        return 0;
    }
}
```

시간복잡도 O(nlogn), 공간복잡도 O(n)

## 막혔던 부분

