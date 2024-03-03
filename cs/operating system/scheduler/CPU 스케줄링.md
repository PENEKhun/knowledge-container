**선점 = Preemptive = 선수 치다**
# 선점 스케줄링
> Preemptive Scheduling

**선점 스케줄링**은 하나의 작업이 실행되는 도중 다른 작업이 도착하면 *우선순위에 따라서 기존 작업을 멈추고 다른 작업을 실행할 수도 있음*
## 알고리즘
[Round Robin 라운드 로빈](Round%20Robin%20라운드%20로빈.md)

*Draft*
*TODO* : https://github.dev/torvalds/linux/tree/master/kernel/sched 에서 kernel > sched > fair.c 가 CFS 관련 코드임. 이런거 내용 담으면 좋을듯??
## 특징
- 우선순위가 높다면 빨리 처리되기 때문에 실시간 시스템에 유용함
# 비선점 스케줄링
> Non-Preemptive Scheduling

**비선점 스케줄링**은 하나의 작업이 실행되는 도중 다른 작업이 도착하면 *일단 원래 하던 작업이 끝나야 다른 작업을 실행함.*
## 알고리즘
*Draft*
## 특징
- 우선순위가 높은 작업이라도, 이미 하던 작업이 완료될 때 까지 기다려야 함

