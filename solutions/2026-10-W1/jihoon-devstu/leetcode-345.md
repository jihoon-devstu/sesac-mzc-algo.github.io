---
status: done
language: java
---

## 접근

- 모음배열을 소문자 , 대문자로 만들어서 indexOf 로 true false 반환하는 메서드 제작
- 가장 왼쪽과 오른쪽을 포인터로 지정하여 좁혀가면서 둘다 모음이면 교환 or 한칸씩 이동

## 풀이

```java
class Solution {
    public String reverseVowels(String s) {
        char[] chars = s.toCharArray();
        int left = 0;
        int right = chars.length - 1;

        while (left < right) {
            if (!isVowel(chars[left])) {
                left++;                 // 왼쪽이 모음이 아니면 한 칸 이동
            } else if (!isVowel(chars[right])) {
                right--;                // 오른쪽이 모음이 아니면 한 칸 이동
            } else {
                // 둘 다 모음이면 교환하고 둘 다 이동
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right] = temp;
                left++;
                right--;
            }
        }

        return new String(chars);
    }

    private boolean isVowel(char c) {
        String vowel = "aeiouAEIOU";
        return vowel.indexOf(c) != -1;
    }
}

```
시간 복잡도 : O(n), 공간 복잡도: O(n)
소요시간 : 80분

## 막혔던 부분
- isVowel 메서드 구현
- 둘다 모음일때 교체한 뒤 추가적으로 이동을 굳이 해야하나 싶었는데 , 이동하지 않으면 메서드에서 무한루프 char[left] 와 char[right]가 여전히 모음이므로. 따라서 끝날때까지 순회 후 while 종료가 필요.
