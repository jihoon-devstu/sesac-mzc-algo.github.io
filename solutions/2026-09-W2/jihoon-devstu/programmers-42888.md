---
status: done
language: java
# 블로그 등 풀이 원문이 있으면 아래 주석을 해제해 입력합니다.
# url: https://example.com/solution
---

## 접근

1. String : String 의 해시맵을 선언하며 참가자의 닉네임 관리하기
    -> HashMap 의 경우 , 같은 키값에 다른 벨류 값을 넣으면 update 되는 매커니즘 활용
2. record 의 경우엔 Leave 시 Nickname이 없기에 split된 배열의 인덱스가 2 , Enter와 Change의 경우 nickname이 붙어 인덱스가 3이므로 해당 부분 주의
3. answer 의 경우엔 Change는 배열에 포함되면 안되므로 , if문으로 Enter와 Leave의 경우에만 배열에 add 하기.

## 풀이

```java
import java.util.HashMap;
import java.util.Map;
import java.util.List;
import java.util.ArrayList;

class Solution {
    

    
    public String[] solution(String[] record) {
        Map<String, String> nicknames = new HashMap<>();
        
        for(String s : record) {
            
            String[] splitRecord = s.split(" ");
            String type = splitRecord[0];
            
            if(type.equals("Enter") || type.equals("Change")){
                String id = splitRecord[1];
                String nickname = splitRecord[2];
                nicknames.put(id,nickname);
            }
        }
        
        
        String[] answer = {};
        List<String> list = new ArrayList<>();
        
        for(String s : record) {
            String[] splitRecord = s.split(" ");
            String type = splitRecord[0];
            
            if(type.equals("Enter")){
                String id = splitRecord[1];
                String nickname = nicknames.get(id);
                
                list.add(nickname+"님이 들어왔습니다.");
            }else if(type.equals("Leave")){
                String id = splitRecord[1];
                String nickname = nicknames.get(id);
                
                list.add(nickname+"님이 나갔습니다.");
            }
        }
        
        answer = list.toArray(new String[0]);
        
        return answer;
    }
}
```

시간 O(N), 공간 O(N)

소요시간: 약 30분

## 막혔던 부분

1. 처음엔 char 로 배열별 첫글자만 따서 if문을 걸었는데 , 그렇게하면 가시성이 너무 안좋고 ID와 NicakName을 저장하는게 2번 일을 하는 것 같아 split 기준으로 type를 지정하였습니다.

2. 주어진 배열과 , answer 로 들어가는 배열의 크기가 다르기 때문에 answer의 크기를 record.length로 지정할 수 없어 따로 ArrayList를 만들고 , 거기에 add 한 다음 마지막에 String 배열로 전환하였습니다.

