> JAVA에서 `synchronized` 키워드로 적용되는 동기화 방법이다.

```java
public synchronized void incrementFailureCount() {
	this.failureCount++;
}
```

# 특징
- 한번에 하나의 스레드만 접근할 수 있다.
- `synchronized` 키워드로 자동으로 락 획득, 해제된다.
