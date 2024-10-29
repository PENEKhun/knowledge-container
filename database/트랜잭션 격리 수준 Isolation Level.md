> 트랜잭션의 [[ACID]]를 보장하기 위해 사용

- Read Committed (Level 1)
	- 대부분 RDBMS에서 기본 적용된 격리수준
	- 한 트랜잭션의 변경을 커밋을 해야 다른 트랜잭션에서 조회 가능
	- ![[Non-Repeatable Read 반복 가능하지 않은 읽기]]

- Repeatable Read (Level 2)
	- 트랜잭션이 실행되기전 커밋된 데이터에 대해서만 조회 가능.
	- ![[Phantom Read|팬텀리드가 발생 가능]]

- SERIALIZABLE
	- 가장 엄격한 격리 수준, 처리성능 가장 낮음.
	- 트랜잭션이 동시에 일어나지 않고, 순차적으로 실행되는 것처럼 동작.