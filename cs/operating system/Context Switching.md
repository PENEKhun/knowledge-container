> 문맥 교환

Context란 번역하면 '(어떤 일의) 맥락, 전후 사정'을 뜻한다.

![[context-switching-point.png]]
> 출처 : 순천향대학교 정보보호학과 운영체제 과목 PDF

Context Switching가 필요한 이유는 [[Concurrent 동시성|다중 프로그래밍]] 환경에서 다른 프로세스로 전환될 때 정보 손실을 없게 하기 위함이다. 그래서 Context Switching이 발생될 때 프로세스를 처리하려고 저장해두었던 Register 정보 등을 불러온다. 이러한 정보들은 [[프로세스 제어 블록]](Process Control Block)에 저장된다.

즉 PCB 정보를 교체하는 과정이라고 할 수 있다.