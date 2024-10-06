# 너비 우선 탐색 (Breadth First Search)
![[BFS.png]]

너비 우선탐색은 
 - 탐색할 때 [[Queue]]를 사용하여, 현재 노드에서 방문 가능한 모든 노드를 큐에 추가하고 탐색함.
 - 모든 노드를 최소한의 횟수로 방문하며 탐색함. 따라서 최소 탐색 거리를 구할 때 사용함.

## 함정 조심
못가는 곳이 있거나 그럴때만 BFS 사용.
그렇지 않다면, 그리디로 해결 할 수 있음.
https://school.programmers.co.kr/learn/courses/30/lessons/12980

## 코드로 확인
### 문제
현수는 송아지를 잃어버렸다. 다행히 송아지에는 위치추적기가 달려 있다.

현수의 위치와 송아지의 위치가 수직선상의 좌표 점으로 주어지면 현수는 현재 위치에서 송아지의 위치까지 다음과 같은 방법으로 이동한다.

송아지는 움직이지 않고 제자리에 있다.

현수는 스카이 콩콩을 타고 가는데 한 번의 점프로 앞으로 1, 뒤로 1, 앞으로 5를 이동할 수 있다.

최소 몇 번의 점프로 현수가 송아지의 위치까지 갈 수 있는지 구하는 프로그램을 작성하세요.

> 예시 입력 : 5 14
> 예시 출력 : 3

### 솔루션
최단 거리를 구해야 하므로, 점프할 수 있는 범위 {1, -1, 5}에 대해서 깊이 우선 탐색을 하면 된다.
그리고 무한루프에 빠질 수 있으므로, 이미 방문한적 있는 노드(내 위치) 에 대해선 더이상 탐색하지 않게 하면 된다.
- 내 위치에서 dx{1, -1, 5}를 각각 더한 값을 큐에 넣어두고, 방문을 기록함.
- dest에 도착할 때 까지, 큐에서 값을 꺼내고, 반복

![[bfs-solution.png]]

```java
public class Main {  
  
  static int targetPos;  
  static int[] d = {1, -1, 5};  
  static int[] visited;  
  
  static int bfs(int myPos) {  
    Queue<Integer> queue = new LinkedList<>();  
    queue.offer(myPos);  
    int result = 0;  
    while (!queue.isEmpty()) {  
      int now = queue.poll();  
      for (int i : d) {  
        int dPos = now + i;  
        if (dPos < 0) {  
          continue;  
        }  
  
        if (visited[dPos] != 0) {  
          continue;  
        }  
  
        visited[dPos] = visited[now] + 1;  
        if (dPos == targetPos) {  
          result = visited[dPos];  
          break;  
        }  
  
        queue.offer(now + i);  
      }  
  
      if (result != 0) {  
        break;  
      }  
    }  
  
    return result;  
  }  
  
  public static void main(String[] args) {  
    Scanner s = new Scanner(System.in);  
    int myPos = s.nextInt();  
    targetPos = s.nextInt();  
    visited = new int[10_001];  
    System.out.println(bfs(myPos));  
  }  
}
```