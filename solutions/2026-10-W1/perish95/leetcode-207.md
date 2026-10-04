---
status: done
language: cpp
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
# 파일명 양식
# programmers-.md  leetcode-.md
---

## 문제 설명

- 수강해야 할 과목의 개수`numCourses`와 선행 강의가 들어있는 `prerequisites` 배열이 주어진다. 
- 선행 강의를 만족하면서 들어야할 과목의 개수를 충족시킬 수 있는지 `bool` 형태로 반환한다.
- ex) prerequisites = {[1,0]} 이면 과목 1을 듣기 위해서 과목 0을 들어야한다. 0 -> 1

## 접근

- **위상정렬**을 이용한 문제이다. 위상 정렬은 방향 그래프에서 모든 정점을 일정한 순서로 나열한 알고리즘이다.
- `prerequisites`에서 인덱스가 가장 낮은 순서대로 graph에 저장한다.
- `visited`의 값이 그대로 0인 인덱스(선행 강의가 없는 강의들)들을 우선 큐에 집어넣는다. 그리고 true, false 판단을 위한 count를 준비한다.
- while문에서 큐에 집어넣은 인덱스(강의)를 꺼내고 graph[강의]에 있는 vector들을 순회하면서 꺼낸 강의가 선행인 강의들의 카운트를 낮춘다.
- 이 때, 값이 0이 된 인덱스들은 큐에 집어넣는다. 꺼내진 강의의 수가 count에 저장되고 count와 numCoursesrk 같을 경우 true 아니면 false

## 풀이

```C++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> visited(numCourses, 0);
        queue<int> q;


        for (auto& p : prerequisites) {
            int course = p[0];
            int prerequisite = p[1];

            graph[prerequisite].push_back(course);
            visited[course]++;
        }

        for (int i = 0; i < numCourses; i++) {
            if (visited[i] == 0)
                q.push(i);
        }

        int count = 0;

        while (!q.empty()) {
            int cur = q.front();

            q.pop();
            count++;

            for (int next : graph[cur]) {
                visited[next]--;

                if (visited[next] == 0)
                    q.push(next);
            }
        }

        return count == numCourses;
    }
};

```

시간복잡도O(V + E) V: 과목 수, E: 선행 강의의 관계 수
소요시간: 약 60분

## 막혔던 부분


