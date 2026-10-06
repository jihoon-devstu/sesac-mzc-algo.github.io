---
status: done
language: java
---

## 접근
- s 를 " " 기준으로 split 하여 배열로 저장
- 해당 배열을 2중 for문으로 순회하며 char와 word 가 같은 패턴이 나오는지 검사


## 풀이

```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");

        if (pattern.length() != words.length) {
            return false;
        }

        int n = words.length;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                boolean sameChar = pattern.charAt(i) == pattern.charAt(j);
                boolean sameWord = words[i].equals(words[j]);

                // 글자가 같은지와 단어가 같은지가 다르면 대응이 깨짐
                if (sameChar != sameWord) {
                    return false;
                }
            }
        }

        return true;
    }
}

```
시간복잡도 : O(m·n) , 공간복잡도 : O(n)

## 막혔던 부분

1. s와 패턴을 일치시키기 위해 링크 시키는 과정에 대한 아이디어
2. 2중포문을 어떤 기준으로 순회 시킬건지