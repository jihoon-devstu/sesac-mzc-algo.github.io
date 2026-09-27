---
status: todo
language: java
---

## 접근

- nums1 배열의 뒤에 nums2 의 요소를 하나씩 붙이기.
- 다 붙이고 나서 정렬하기.


## 풀이

접근방식과 동일.

```java
import java.util.*;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        for(int i=0; i<n; i++){
            nums1[i+m] = nums2[i];
        }

        Arrays.sort(nums1);
    }
}

```


시간 O((m+n) log(m+n)) , 공간 O(m+n)
소요시간 : 30분


## 막혔던 부분

