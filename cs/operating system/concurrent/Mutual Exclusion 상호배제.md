[[Critical Section 임계구역|임계구역]]에 한번의 하나의 스레드만 접근할 수 있도록 제한 함.

```java
// synchronized를 통해 임계 구역을 보호하여 상호 배제 보장
public synchronized void increment(){ 
	counter++;
}
```
