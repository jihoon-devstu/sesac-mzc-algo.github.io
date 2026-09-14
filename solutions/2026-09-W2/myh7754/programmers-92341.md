---
status: done
language: java
---

## 접근

1. 먼저 들고 있어야 할 상태를 정한다: 주차 중인 차의 입차 시각(`HashMap`), 차량별 누적 주차 시간(`TreeMap`).
2. 시각을 분 단위로 바꾼 뒤, `IN`이면 입차 시각을 기록하고 `OUT`이면 이번 주차 시간을 누적에 더한다.
3. 순회가 끝난 뒤 `inTime`에 남아 있는 차는 출차 기록이 없는 차이므로 23:59(1439분)에 나간 것으로 정산한다.
4. 누적 시간으로 요금을 계산한다. 기본 시간 이하면 기본 요금, 초과분은 단위 시간으로 올림해서 과금한다.
5. `TreeMap`을 써서 차량 번호 오름차순으로 바로 결과를 만든다.

## 풀이

```java
import java.util.*;

class Solution {
    public int[] solution(int[] fees, String[] records) {

        // ── [1] 상태 정의 ───────────────────────────────
        // 문제를 풀기 전에 "무엇을 들고 있어야 하는가"부터 정한다.
        // 주차 중인 차의 입차 시각 / 차량별 누적 시간, 두 가지면 충분하다.
        Map<String, Integer> inTime = new HashMap<>();   // 아직 안 나간 차: 차량번호 → 입차 시각
        Map<String, Integer> total  = new TreeMap<>();   // 차량번호 → 누적 분 (TreeMap이라 번호순 자동 정렬)

        // ── [2] 기록 순회: 누적 시간 쌓기 ───────────────
        for (String record : records) {
            String[] token = record.split(" ");
            int time = toMinutes(token[0]);              // "HH:MM" → 분 단위로 통일
            String car = token[1];

            if (token[2].equals("IN")) {
                // 입차: 시각 기록 + 차량 등록(누적값 없으면 0으로 초기화)
                inTime.put(car, time);
                total.putIfAbsent(car, 0);
            } else {
                // 출차: 이번 회차 주차 시간을 누적에 더하고, 주차 중 목록에서 제거
                int parked = time - inTime.remove(car);
                total.put(car, total.get(car) + parked);
            }
        }

        // ── [3] 예외 처리: 안 나간 차 정산 ──────────────
        // 순회가 끝난 뒤 inTime에 남아 있는 = 출차 기록이 없는 차량.
        // 23:59(=1439분)에 나간 것으로 간주한다.
        for (Map.Entry<String, Integer> e : inTime.entrySet()) {
            total.put(e.getKey(), total.get(e.getKey()) + (1439 - e.getValue()));
        }

        // ── [4] 출력 변환: 누적 시간 → 요금 배열 ────────
        int[] answer = new int[total.size()];
        int idx = 0;
        for (int minutes : total.values()) {             // TreeMap이라 번호 오름차순으로 나옴
            answer[idx++] = calcFee(fees, minutes);
        }
        return answer;
    }

    // [보조] 시각 파싱: 시:분 → 분
    private int toMinutes(String hhmm) {
        String[] t = hhmm.split(":");
        return Integer.parseInt(t[0]) * 60 + Integer.parseInt(t[1]);
    }

    // [보조] 요금 계산: 기본 시간 이하면 기본 요금, 초과분은 단위 시간당 올림 과금
    private int calcFee(int[] fees, int minutes) {
        int baseTime = fees[0], baseFee = fees[1], unitTime = fees[2], unitFee = fees[3];
        if (minutes <= baseTime) return baseFee;

        int over = minutes - baseTime;
        int units = (over + unitTime - 1) / unitTime;    // 정수 올림
        return baseFee + units * unitFee;
    }
}
```

시간 O(N log M), 공간 O(M) (N = 기록 수, M = 차량 수)

## 막혔던 부분

1. 입·출차할 때마다 요금을 매기는 게 아니라, 하루 동안의 누적 주차 시간을 모두 더한 뒤 한 번에 요금을 계산해야 한다는 점
