### Hashmap  
---  

#### Hashmap 특징  
- null key와 null value를 모두 허용  
- 동기화 보장하지 않는다.  
- 데이터의 순서를 보장하지 않는다.  
- 중복된 key 값을 허용하진 않지만, 중복된 값(value) 허용  

#### Hashmap API  
- put(K key, V value)  
- putAll(Map<? extends K,? extends V> m)  
- get(Object key)  
- remove(Object key)  
- clear()  
- isEmpty()  
- keySet()  
- values()  
- containsKey(Object key)  
- containsValue(Object value)  
- replace(K key, V value)  
- getOrDefault(Object key, V defaultValue)  

##### keySet()  
- Hashmap에 저장된 key들을 Set 객체로 리턴해준다.  

##### getOrDefault()  
- getOrDefault(Object key, V defaultValue)  
- 찾는 key가 존재하면 찾는 키의 값(value)를 반환하고, 없다면 기본 값(dafaultValue)을 반환한다.  


#### 알고리즘 문제 - 프로그래머스  
- [완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)  

- 조건  
 - 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.  
 - completion의 길이는 participant의 길이보다 1 작습니다.  
 - 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.  
 - 참가자 중에는 동명이인이 있을 수 있습니다.  

- 조건으로 볼 때, 완주하지 못한 선수는 항상 1명  
- 각 배열을 순서대로 정렬해서 일치하지 않는 인덱스의 선수를 return  
- 해당 코드는 다른사람의 풀이인데 사실 hashmap으로 풀생각도 안해봤다..  

``` java
import java.util.HashMap;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        HashMap<String, Integer> hm = new HashMap<>();

        for(String player : participant) hm.put(player, hm.getOrDefault(player, 0) + 1);
        for(String player : completion) hm.put(player, hm.get(player) - 1);

        for (String key : hm.keySet()) {
            if (hm.get(key) != 0){
                answer = key;
            }
        }
        return answer;
    }
}
```
{: .notice--primary}  

- 배열 정렬로 풀어본 풀이 코드  

``` java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        Arrays.sort(participant);
        Arrays.sort(completion);

        int i;
        for ( i=0; i<completion.length; i++){

            if (!participant[i].equals(completion[i])){
                return participant[i];
            }
        }
        return participant[i];
    }
}
```
{: .notice--primary}  

&nbsp;  
&nbsp;  
[참고]  
<https://codechacha.com/ko/java-map-hashmap/>  
