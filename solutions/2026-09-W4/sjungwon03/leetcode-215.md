---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

- 숫자 내림차순 정렬
- k번째로 큰 수 반환

## 풀이

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        List<Integer> list = new ArrayList(nums.length);

        for(int i = 0; i<nums.length; i++){
            list.add(nums[i]);
        }

        list.sort(Comparator.reverseOrder());

        return list.get(k - 1);
    }
}
```

시간복잡도 O(nlogn), 공간복잡도 O(n)

## 막혔던 부분

