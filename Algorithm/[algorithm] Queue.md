## Queue  

### Queue 특징  
- 먼저 들어온 데이터가 가장 먼저 나가는 구조  
- FIFO (First In First Out)  
- 순서대로 처리되는 자료구조  

### Queue 선언  
- LinkedList 활용  
- Queue 클래스는 멀티 스레드 환경에서 동기화가 적용되어 있지 않다.  
- 이러한 문제를 해결하기 위해 제공되는 클래스가 <b>ConcurrentLinkedQueue</b>  

``` java
import java.util.Queue;
import java.util.LinkedList;
import java.util.concurrent.ConcurrentLinkedQueue;

Queue<Integer> queue_1 = new LinkedList<>();
Queue<Integer> queue_2 = new ConcurrentLinkedQueue<>();
```

### 알고리즘 문제 - 프로그래머스  
- [다리를 지나는 트럭](https://programmers.co.kr/learn/courses/30/lessons/42583)  

- 조건  
  * bridge_length는 1 이상 10,000 이하입니다.  
  * weight는 1 이상 10,000 이하입니다.  
  * truck_weights의 길이는 1 이상 10,000 이하입니다.  
  * 모든 트럭의 무게는 1 이상 weight 이하입니다.  

- queue 객체  
- forEach를 통해 트럭의 수만큼 반복한다.  
- 조건1. queue가 비어있는 경우, 트럭 무조건 진입 가능하기때문에 바로 큐에 add()  
- 조건2. queue 사이즈가 다리의 길이와 같은 경우, poll()  
- 조건3. 트럭이 다리 위에 있지만 queue가 가득 차 있지 않은 상태  
- 다리위에 있는 트럭의 무게 + 추가 될 트럭 무게 합이 weights를 초과하는지 조건 검사  
- weights 보다 크다면 새로운 트럭 진입 불가, queue에 0을 넣어서 이미 queue에 있는 트럭이 다리 지나가도록 해준다.  

``` java
import java.util.Queue;
import java.util.concurrent.ConcurrentLinkedQueue;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0;
        Queue<Integer> queue = new ConcurrentLinkedQueue<>();
        int sum = 0;

        for(int t : truck_weights) {
            while(true) {
                if(queue.isEmpty()) {
                    queue.add(t);
                    sum += t;
                    answer++;
                    break;
                } else if(queue.size() == bridge_length) {
                    sum -= queue.poll();
                } else {
                    if((sum + t) > weight) {
                        answer++;
                        queue.add(0);
                    } else {
                        queue.add(t);
                        sum += t;
                        answer++;
                        break;
                    }
                }
            }
        }

        return answer + bridge_length;
    }
}
```
