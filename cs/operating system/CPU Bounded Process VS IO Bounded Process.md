# ![[CPU Bounded Process]]
# ![[Draft) IO Bounded Process]]

# CPU Bound와 I/O Bound
만일 동시성이 빈번히 일어나는 시스템을 운영할때, CPU와 I/O 작업 중 무엇의 작업량이 많은지 확인 해야 한다. 이후에 적절한 대응을 하여 최적화를 할 수 있다.

## CPU Burst가 잦은 프로세스
- 작업 병렬 처리
- 알고리즘 최적화

등..
## I/O Burst가 잦은 프로세스
- 더 좋은 외부 장치 도입 (I/O 작업이 빨리 끝나도록)
- I/O 스케줄링 최적화
	- 더 중요한 I/O 작업부터 처리되도록 함

등 ..