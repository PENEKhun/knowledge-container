- Atomicity 원자성 (All do Or All Nothing)
	- 모든 작업이 반영되거나, 모두 롤백되는 특성
	
- Consistency 일관성
	- 트랜잭션이 성공적으로 완료되면, 항상 일관성 있는 DB 상태가 유지

- Isolation 고립성
	- 둘 이상의 트랜잭션 간 명령의 간섭 정도
	- 수행 중인 트랜잭션은 완전히 종료될때 까지, 다른 트랜잭션에서 수행 결과를 참조할 수 없음.

- Durability 영속성
	- 한번 반영된 데이터는 영구적으로 적용