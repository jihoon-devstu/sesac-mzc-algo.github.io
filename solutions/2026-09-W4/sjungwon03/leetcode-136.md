---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

- map에 숫자 개수 저장
- 한번만 나온 숫자 리턴

## 풀이

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();

        for(int i = 0; i < nums.length; i++){
            if(map.get(nums[i]) != null){
                map.put(nums[i], 2);
            }else {
                map.put(nums[i], 1);
            }
        }

        for(Integer keys : map.keySet()){
            if(map.get(keys) == 1){
                return keys;
            }
        }

        return -1;
    }
}
```

시간복잡도 O(n), 공간복잡도 O(n)

## 막혔던 부분

