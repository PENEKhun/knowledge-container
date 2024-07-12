"Tell, Don't Ask(*TDA*)" 원칙은 객체의 상태를 묻지말고, 원하는 동작을 시키는 것이다.
아래는 `Ticket`의 만료일을 체크하는 코드이다.
```java
if (ticket.getExpiredAt().isBefore(LocalDateTime.now()) && !ticket.unlimited) {  
  System.out.println("티켓이 만료되었습니다.");  
} else {  
  System.out.println("티켓이 유효합니다.");  
}
```
티켓을 이용하는 객체(`Caller`)가 티켓(`Callee`)의 내부구현을 뻔히 알고 있게 된다.
이는 OOP관점에서 잘못된 코드이다. 따라서 TDA원칙에 따라 다음처럼 은닉할 수 있다.
```java
public class Ticket {  
  
  private String name;  
  private LocalDateTime expiredAt;  
  private boolean unlimited;  
  private int price;  
    
  public boolean isExpired() {  
    return expiredAt.isBefore(LocalDateTime.now()) && !unlimited; // 추가된 코드
  }  
}
```

```java
if (ticket.isExpired()) {  
  System.out.println("티켓이 만료되었습니다.");  
} else {  
  System.out.println("티켓이 유효합니다.");  
}
```

이 원칙을 따르면 객체의 내부 구현을 알 필요 없이 그저 원하는 동작을 시키기만 하면 된다. 이로 인해 객체 간의 결합도가 낮아지게 된다.
또한 티켓 만료에 대한 처리로직이 변경된다면 티켓의 `isExpired()`만 수정하면 되기에 유지보수에 용이하다. 