여러 [[Thread 쓰레드|쓰레드]]가 공유된 자원에 접근하는 코드 영역

```java
public synchronized void incrementFailureCount() {
	// 임계영역
	this.failureCount++;
}
```

임계영역은 최대한 작은 사이즈로 정해야함.

```java
private int failureCount = 0;

public void incrementFailureCount() {
    // 임계영역 최소화: 필요한 부분만 동기화
    synchronized (this) {
        this.failureCount++;
    }
    
	// 출력작업엔 락이 필요없음.
    System.out.println("Failure count incremented.");
}

```

