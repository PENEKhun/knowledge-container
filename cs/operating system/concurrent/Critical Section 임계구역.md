여러 스레드가 공유된 자원에 접근하는 코드 영역

```java
public synchronized void incrementFailureCount() {
	// 임계영역
	this.failureCount++;
}
```