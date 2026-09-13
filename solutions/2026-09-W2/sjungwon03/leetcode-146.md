---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

LRU Cache 문제 해석
- capacity 크기로 초기화
- get -> 값이 있으면 값 반환, 없으면 -1 반환
- put -> key에 해당하는 값이 있으면 업데이트, 없으면 key-value를 캐시에 저장. 만약 cache에 저장된 요소가 capacity를 넘어서면 가장 오래 사용되지 않은 원소를 제거
- get, put은 O(1) 시간복잡도를 가져야함

- 맵과 연결리스트를 사용 - key<->value는 별도 타입으로 관리(포인터)
- 맵 -> key <-> node
- 연결리스트 -> (key<->value) Node 리스트 -> 맨 뒤 요소를 탐색할 수 있도록 tail이 있는 연결리스트
- 맵 key가 capacity를 넘어가면 연결리스트 맨 뒤 요소(tail->prev) 삭제 및 해당 key를 map에서도 제거


## 풀이

```cpp
#include <unordered_map>

using namespace std;

class Node {
public:
    int key;
    int value;
    Node* prev;
    Node* next;

    Node(int key, int value) {
        this->key = key;
        this->value = value;
        this->prev = nullptr;
        this->next = nullptr;
    }
};

class LRUCache {
private:
    int capacity;

    unordered_map<int, Node*> map;

    Node* head;
    Node* tail;

public:
    LRUCache(int capacity) {
        this->capacity = capacity;

        head = new Node(0, 0);
        tail = new Node(0, 0);

        head->next = tail;
        tail->prev = head;
    }

    int get(int key) {
        if (map.find(key) == map.end()) {
            return -1;
        }

        Node* node = map[key];

        remove(node);
        addFirst(node);

        return node->value;
    }

    void put(int key, int value) {
        if (map.find(key) != map.end()) {
            Node* node = map[key];

            node->value = value;

            remove(node);
            addFirst(node);

            return;
        }

        Node* node = new Node(key, value);

        map[key] = node;
        addFirst(node);

        if (map.size() > capacity) {
            Node* oldNode = tail->prev;

            remove(oldNode);
            map.erase(oldNode->key);

            delete oldNode;
        }
    }

private:
    void remove(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }

    void addFirst(Node* node) {
        node->next = head->next;
        node->prev = head;

        head->next->prev = node;
        head->next = node;
    }
};
```
- get, put 시간복잡도 O(1)
- 공간복잡도 -> O(capacity)

### AI 풀이
```cpp
#include <unordered_map>
#include <list>

using namespace std;

class LRUCache {
private:
    int capacity;

    // key, value
    list<pair<int, int>> cache;

    // key -> list iterator
    unordered_map<int, list<pair<int, int>>::iterator> map;

public:
    LRUCache(int capacity) {
        this->capacity = capacity;
    }
    
    int get(int key) {
        if (map.find(key) == map.end()) {
            return -1;
        }

        auto it = map[key];

        int value = it->second;

        // 최근 사용한 항목을 앞으로 이동
        cache.erase(it);
        cache.push_front({key, value});

        map[key] = cache.begin();

        return value;
    }
    
    void put(int key, int value) {
        // 이미 존재하는 경우
        if (map.find(key) != map.end()) {
            cache.erase(map[key]);
        }

        // 가장 최근 사용 위치에 추가
        cache.push_front({key, value});
        map[key] = cache.begin();

        // capacity 초과 시 가장 오래된 항목 제거
        if (cache.size() > capacity) {
            int oldKey = cache.back().first;

            cache.pop_back();
            map.erase(oldKey);
        }
    }
};
```
- iterator는 C++ STL 자료구조에서 원소를 가리키는 포인터 비슷한 객체라고 보면 됩니다.

## 막혔던 부분

- AI 풀이에서 iterator 문법을 새로 알게되었습니다.
- 해시 충돌이 극단적인 경우 O(N)이 될 수 있다는 점도 AI를 통해 학습