
|  | [Process](Process.md) | [Thread](Thread.md) |
| ---- | ---- | ---- |
| 하나가 뻗으면 | 자식 프로세스 하나가 문제 발생시, 다른 프로세스에게 영향을 미치지 않음. (안정성을 확보할 수 있다) | 하나의 쓰레드가 문제 발생시, 다른 쓰레드에게도 영향을 미침. 최악의 경우 프로세스 자체가 뻗을 수도 있다. |
| 통신 비용 | 프로세스간 통신은 복잡하고 오버헤드가 크다 | 오버헤드가 작다 |
| [[Context Switching]]이 발생할 때 | 프로세스간 문맥 전환시 레지스터, 캐시메모리 초기화 등 무거운 작업으로 인한 시간적 비용이 많이 발생한다 | 프로세스의 메모리 영역을 공유하기 때문에 시간이 빠르고, 리소스를 효율적으로 사용한다. |
|  |  | 공유 메모리 접근시 동기화 문제가 발생한다. |