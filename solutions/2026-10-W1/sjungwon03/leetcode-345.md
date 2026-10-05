---
status: done
language: javascript
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명

- 문자열에 존재하는 모음의 순서 뒤집기

## 접근

- 투포인터를 두고 모음인 경우 순서 뒤집기

## 풀이

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
    let i = 0;
    let j = s.length - 1;

    const vowels = new Set(['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']);

    const sArr = s.split("");

    while(i <= j){
        if(vowels.has(sArr[i]) && vowels.has(sArr[j])){
            const tmp = sArr[i];
            sArr[i] = sArr[j];
            sArr[j] = tmp;
            i++;
            j--;
            continue;
        }
        if(!vowels.has(sArr[i])){
            i++;
        }
        if(!vowels.has(sArr[j])){
            j--;
        }
    }

    return sArr.join("");
};

```

시간복잡도 O(n)

## 막혔던 부분
