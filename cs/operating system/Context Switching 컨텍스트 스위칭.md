# 정의
> Context : (어떤 일의) 맥락, 전후 사정, 문맥
> Context Switch : 문맥 교환

Context Switching은 한개의 코어에서 여러개의 Job을 번갈아 가며 수행되는 그 시점을 말한다.

![[context-switching-point.png]]
> 출처 : 순천향대학교 정보보호학과 운영체제 과목 PDF
# 필요한 이유
[[Concurrent 동시성|다중 프로그래밍]] 환경에서 다른 프로세스로 전환될 때 정보 손실을 없게 하기 위함이다. 그래서 Context Switching이 발생될 때 프로세스를 처리하려고 저장해두었던 Register 정보 등을 불러온다. 이러한 정보들은 [[프로세스 제어 블록 (PCB)]](Process Control Block)에 저장된다.

즉 PCB 정보를 교체하는 과정이라고 할 수 있다.
# 단점
![[context-switching-do.png]]
PCB 정보를 저장하고 꺼내오는 과정 동안 CPU는 프로세스의 작업을 처리하는게 아닌 다음 프로세스 처리를 위한 일련의 준비 활동을 하고 있다. 따라서 Context Switch가 수행될 때 마다 [[Overhead 오버헤드|오버헤드]]가 발생한다고 말할 수 있다.

따라서, 한개의 코어에서 5초짜리 Job이 3개 수행 되면 $5 \times 3$ 초보다 넘는 시간이 걸린다.

![[babel-god.png]]
> ???: Context Switching은 조상님이 해주시냐?
## 최적화 방법
완전 엄청난 동시성 시스템이라면 이러한 [[Overhead 오버헤드|오버헤드]]는 계속 중첩될 것이다. 따라서 적절한 최적화 전략이 필요할 수 있다.
### 적절한 CPU 스케줄링 알고리즘 선택
[[CPU 스케줄링]] 알고리즘을 통해 Context Switching의 횟수, 시기 등을 제어할 수 있다. 사용되는 환경에 맞게 적절한 [[CPU 스케줄링]] 알고리즘을 사용하면 Context Switching 비용을 절감할 수 있다.

예시로 실시간 처리가 매우 중요한 제어시스템의 경우엔 중요도에 따른 Job 처리가 중요할 테고, 그렇지 아니하면 자주 쓰이는 [[Round Robin 라운드 로빈|라운드 로빈]]을 사용하면 될 것이다.
### 멀티코어 아키텍처 사용
멀티코어 아키텍처를 사용하면 여러 작업을 병렬로 수행하여, 대충 계산하면 기존 오버헤드 비용 / 코어 갯수로 만큼 시간을 절감할 수 있다.