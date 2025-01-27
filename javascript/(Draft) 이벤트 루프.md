*TODO: 내용 보강 필요한 것* 
*이벤트 큐, 마이크로태스크, 실제 동작 혹은 구현 느낌 등*

# 주의사항
이벤트 루프의 핵심은 JS가 아닌, 브라우저(혹은 프레임 워크)이다.
Node.js의 경우엔 [libuv](https://github.com/libuv/libuv) 내장 라이브러리가 처리함.

# 설명
만약에 JS에 [[(이벤트 루프]]가 없었다면, 코드(명령)을 순차적으로 실행시키기 어려울 것이다.
- **문제점:**
    - 자바스크립트는 싱글 스레드 언어임.
    - 따라서 시간이 오래 걸리는 동기 작업을 실행하면 프로그램이 멈춘 것처럼 보일 수 있음.
- **해결책:**
    - 이러한 문제를 피하기 위해 자바스크립트는 비동기 작업을 허용하며, 이를 효율적으로 관리하기 위해 이벤트 루프가 사용됨.
- **이벤트 루프의 역할:**
    - 비동기 작업이 실행되면, 해당 작업은 콜백 함수를 이벤트 큐에 등록.
    - 작업이 완료되면, 이벤트 루프는 이벤트 큐에서 콜백을 가져와 콜 스택이 비어 있을 때 실행.
- **결과:**
    - 이 방식으로 비동기 작업이 효율적으로 관리되고, 프로그램이 멈추지 않고 계속 진행되면서도 사용자의 명령에 즉시 반응할 수 있음.

# Ref
- https://nodejs.org/ko/learn/asynchronous-work/event-loop-timers-and-nexttick
- https://inpa.tistory.com/entry/%F0%9F%94%84-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-%EA%B5%AC%EC%A1%B0-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC
- https://velog.io/@devmag/Javascript-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%8B%B1%EA%B8%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%B8%EA%B0%80
