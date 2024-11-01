char[]을 Map이나 Set으로 쓸땐, 그냥 String으로 만들어 넣어라
-> 예상처럼 동작하지 않기 때문


# 플랫폼 별 팁
## 잡다
N단계로 이뤄진 요구사항 수정 문제는
이전 정답 코드를 계속 복붙 + 주석으로 관리하는게 좋을듯
## 소프티어
백준처럼 빠른 입출력 알고 있어야함.
```java
import java.util.*;
import java.io.*; // io 중요

BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); // InputStreamReader임 주의
```
## 프로그래머스
- 그냥 `import java.util.*` 만 추가하고 하면됨.
- 메소드 파라미터명이나, 리턴 타입 (int[] -> Integer[]) 이런식으로 변경해도 됨.