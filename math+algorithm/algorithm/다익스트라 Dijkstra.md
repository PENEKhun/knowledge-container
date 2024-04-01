![](https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif)

음이 아닌 가중치가 주어졌을때, 가장 최단 경로를 구하는 알고리즘.
[[너비 우선 탐색 BFS|BFS]]와 [[동적 계획법 DP|DP]]의 memo가 적절히 섞인 형태로 구현된다.

 일단 중요한 점
 1. 출발지가 정해져야함. 그리고 출발지를 제외한 모든 거리는 *INF*로 초기화 해야 함.
	 만약, 모든 위치에서의 거리를 구해야하면 [[플로이드 워셜 Floyd Warshall]]을 사용해야 함.
 1. **가중치에 음수가 있으면 안됨. 0까진 됨.** (최소값 갱신을 확실하게 할 수 없음)
	만약, 음의 가중치가 있다면 [[벨만-포드]]를 사용해야 한다.
 1. 가까운 간선부터 방문하기 때문에, 우선순위 큐가 사용됨.
 2. 같은 방향의 간선이 여러개 있을 수도 있어서 ArrayList<ArrayList<Edge\>\> 이런식으로 사용함
 3. 갱신 후 큐에 다음 간선을 넣을 때, 누적 가중치를 바탕으로 넣어야함. 그래야 효율적으로 찾을 수 있음.

```java
PriorityQueue<Edge> queue = new PriorityQueue<>();  
Arrays.fill(memo, Integer.MAX_VALUE); // 그 외 지점은 INF
memo[start] = 0; // 시작 지점은 반드시 0
queue.offer(new Edge(start, 0)); 
  
while (!queue.isEmpty()) {  
  Edge edge = queue.poll();  
  int from = edge.to;  
  
  for (Edge next : edges.get(edge.to)) {  
    if (memo[next.to] > memo[from] + next.weight) {  
      memo[next.to] = memo[from] + next.weight;  
      queue.offer(new Edge(next.to, memo[next.to]));  
      /*
	      그냥 next.weight로 하면 안됨.
	      반드시 memo[next.to]로 넣어야함. (누적 가중치 바탕)
	      그래야 효율적으로 찾을 수 있음.
      */
    }  
  }  
}
```
 