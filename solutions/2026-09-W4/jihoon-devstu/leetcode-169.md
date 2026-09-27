---
status: todo
language: java
---

## 접근

맵을 생성하여 nums[i] 번째의 갯수만큼 value 에 put한 뒤
nums.length의 2분의1만큼 진행되면 return

## 풀이

접근방식과 동일.

```java
import java.util.*;

class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            int count = map.getOrDefault(num, 0) + 1;
            if (count > nums.length / 2) return num;
            map.put(num, count);
        }
        return -1;
    }
}

```

시간 O(n), 공간 O(n)

## 막혔던 부분

