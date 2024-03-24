
```java
public static void doSomething(int primitive) {  
  primitive = 999999;  
}  
  
public static void main(String[] args) {  
  int primitive = 10;  
  doSomething(primitive);  
  System.out.println("value: " + primitive);
}
```

위 코드의 결과는 `value: 10` 이다. **값이 변경되지 않았다.**

```java
public static void doSomething(List<String> list) {  
  list.add("do something added....");  
}

public static void main(String[] args) {  
	ArrayList<String> list = new ArrayList<>();  
	doSomething(list);  
	System.out.println("list: " + list);
}
```

위 코드의 결과는 `list: [do something added....]`이다. **값이 변경되었다.**

엥??? 이렇게 되면....
"Java는 [[Primitive Type과 Reference Type#Primitive Type - 원시형| Primitive Type]] 일땐 Call by value로 동작하고, [[Primitive Type과 Reference Type#Reference Type| Reference Type]] 일땐 Call by reference로 동작하는 게 아닌가?" 라는 의문이 들 수 있다.

일단 결론부터 말 하자면 **Java는 100% Call by value이다.**


# Call by value인 이유
## 인자가 primitive 타입일 때

아까와 같은 코드이다.
```java
public static void doSomething(int primitive) {  
  primitive = 999999;  
}  
  
public static void main(String[] args) {  
  int primitive = 10;  
  doSomething(primitive);  
  System.out.println("value: " + primitive);
}
```

일전에, [[Primitive Type과 Reference Type#Primitive Type - 원시형| Primitive]] 타입은 스택에 값이 저장된다고 했다.
여기서 `doSomething()`으로 값을 넘기게 되면
스택에 일단 아래 처럼 데이터가 있을 것이다. _(스택 프레임 등은 생략함.)_

|     |
| --- |
|     |
| 10  |
| 10  |

이제 `primitive = 999999`가 실행되면, 아래처럼 스택이 변경될 것이다.

|       |
| ----- |
|       |
| 99999 |
| 10    |

이후 `doSomething()`이  끝나면 main함수로 복귀할 것이다. 그러면 스택은 다음처럼 될 것이다.

|     |
| --- |
|     |
| 10  |

확실히 Call by value인 것이다.

## 인자가 Reference Type일 때
아까와 같은 코드이다.

```java
public static void doSomething(List<String> list) {  
  list.add("do something added....");  
}

public static void main(String[] args) {  
	ArrayList<String> list = new ArrayList<>();  
	doSomething(list);  
	System.out.println("list: " + list);
}
```

일전에, [[Primitive Type과 Reference Type#Reference Type| Reference]] 타입은 힙에 값이 저장된다고 했다.
실질적인 값이 힙에 저장된다고 한들, 변수의 메모리 정보는 Stack에 저장하고 있을 것이다.

따라서 `doSomething()`이 실행되면 스택은 아래처럼 예상 해볼 수 있다.

|                                            |
| ------------------------------------------ |
| (doSomething 내부) variable address (0x1234) |
| (main 함수 내부) variable address (0x1234)     |

분명 primitive 타입처럼 복사가 되는것 처럼 보인다.
하지만, 실질적으로 가르키는 주소값은 똑같기 때문에 복사를 해도 같은 곳을 바라보게 된다.
그래서 (doSomething 내부) 리스트에 추가를 하게되면, (main 함수 내부) 리스트에 추가가 되는 것이다.