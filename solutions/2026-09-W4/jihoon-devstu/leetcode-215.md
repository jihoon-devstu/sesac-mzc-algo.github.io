---
status: done
language: java
---

## 접근

sort를 쓰지 못하니 , 버블정렬을 코드로 구현.
그 이후 k번째 수 반환

## 풀이

접근방식과 동일.

```java
import java.util.*;

class Solution {
    public int findKthLargest(int[] nums, int k) {
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = 0; j < nums.length - 1 - i; j++) {
                if (nums[j] < nums[j + 1]) {
                    int tmp = nums[j];
                    nums[j] = nums[j + 1];
                    nums[j + 1] = tmp;
                }
            }
        }
        return nums[k-1];
    }
}

```

시간복잡도 O(n²), 공간복잡도 O(1)

소요 시간 : 20분

## 막혔던 부분

