---
status: done
language: java
---

## 접근
- Array 를 sort 로 정렬
- 2 포인터로 가운데부터 왼쪽 , 오른쪽으로 한칸씩 이동하며 조건과 일치할때까지 이동하고 정답 후보 반환


## 풀이

```java
import java.util.Arrays;

class Solution {
    public int findLHS(int[] nums) {
        Arrays.sort(nums);
        int left = 0;
        int answer = 0;

        for (int right = 0; right < nums.length; right++) {
            // 구간의 최댓값 - 최솟값이 1보다 크면 left를 당겨서 구간을 줄인다
            while (nums[right] - nums[left] > 1) {
                left++;
            }

            // 차이가 정확히 1일 때만 정답 후보 
            if (nums[right] - nums[left] == 1) {
                int length = right - left + 1;
                // 현재 구간이 지금까지의 최고 기록보다 길면 갱신
                if (length > answer) {
                    answer = length;
                }
            }
        }

        return answer;
    }
}

```
시간 O(n log n), 공간 O(1)
## 막혔던 부분

소요시간 : 60분
투포인터 첫 공부 후 처음 접목시키는 방향에서 right - left 조건으로 >1과 =1 구하는 식을 접목시키는 과정이 생소했음.