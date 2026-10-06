---
status: done
language: java
---

## 접근

- Map 을 구현하여 prev 값을 기억.
- for문에서 i - prev 값으로 비교하여 true or false 반환

## 풀이

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> lastIndex = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            Integer prev = lastIndex.get(nums[i]);  

            if (prev != null && i - prev <= k) {
                return true;
            }

            lastIndex.put(nums[i], i);
        }

        return false;
    }
}

```
시간 복잡도 : O(n), 공간 복잡도: O(n)
소요시간 : 60분

## 막혔던 부분
- 도저히 투포인터를 직접 구현해서 풀이할 수 있는 방식이 떠오르지 않아서 hashmap 사용.
