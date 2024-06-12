![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Floyd-Warshall_example.svg/1200px-Floyd-Warshall_example.svg.png)


한 출발지에 대한 최소거리를 구하는 [[다익스트라 Dijkstra|다익스트라]]와 달리,
모든 지점에서 최소거리를 구하는 알고리즘이다.

$$
D_{ab} = min (D_{ab}, \; D_{ak} + D_{kb})
$$
## 주의사항
1. 초기에 모든 값이 *INF*로 초기화 되어야 함.

## 코드 예시

```java
for (int goThrough = 1; goThrough <= cityCnt; goThrough++) {  
  for (int start = 1; start <= cityCnt; start++) {  
    for (int end = 1; end <= cityCnt; end++) {  
  
      if (result[start][goThrough] == Integer.MAX_VALUE) {  
        continue;  
      }  
  
      if (result[goThrough][end] == Integer.MAX_VALUE) {  
        continue;  
      }  
  
      result[start][end] =  
          Math.min(result[start][end],  
              result[start][goThrough] + result[goThrough][end]);  
    }  
  }  
}
```


## 관련 문제
- [케빈 베이컨의 6단계 법칙](https://www.acmicpc.net/problem/1389)