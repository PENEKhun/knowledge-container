> PCB (Process Control Block)

운영체제가 프로세스들을 관리하기 위해 **프로세스마다 유지하는 정보**를 담는 [[Kernel 커널]] 내 자료구조이다.
![[pcb.png]]
> [출처](https://velog.io/@turningtwenty/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COperating-System-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EA%B4%80%EB%A6%AC)

```mermaid
graph TD
    PCB[PCB]
    TCB1[TCB]
    TCB2[TCB]
    TCB3[TCB]

    PCB --> TCB1
    PCB --> TCB2
    PCB --> TCB3

```
또한 한개의 PCB 내에는 여러개의 [[TCB]]를 포함하고 있다.
