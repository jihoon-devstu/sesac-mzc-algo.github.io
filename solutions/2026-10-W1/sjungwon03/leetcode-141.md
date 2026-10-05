---
status: done
language: typescript
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명

- 주어진 연결리스트에 사이클이 존재하는지 찾기

## 접근

- set에 접근한 노드 저장, next가 set에 존재하는지 확인

## 풀이

```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function hasCycle(head: ListNode | null): boolean {
    const set = new Set();

    let cur = head;
    while(cur != null){
        set.add(cur);
        if(cur.next != null && set.has(cur.next)){
            return true;
        }
        cur = cur.next;
    }

    return false;
};

```

시간복잡도 O(n)

## 막혔던 부분
