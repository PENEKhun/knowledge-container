JAVA에서 값 타입을 나타낼 때 원시형(*Primitive Type*)과 참조형(*Reference Type*) 두가지가 있다.

## Primitive Type - 원시형
원시(原始)는 사전적으로 **'처음 그대로의'** 를 의미한다.  말 그대로, 값만 표현하는 기본적인 데이터 타입이다.
- *int*, *boolean*, *double*, *char* ...
보다시피 이들은 어떠한 기능을 가진 *Class*, *Object* 형태가 아니다. 순수히 값만 나타낸다. ($\therefore$ 스택 프레임을 직접 확인해보면, 실제 값들이 메모리에 적재되어 있다)

또한 원시형은 데이터 사이즈가 컴파일 시점에 추론이 가능해서 값이 *Stack*에 저장된다.
- *int* -> 4Byte
- *boolean* -> 1Byte
- ... 
## Reference Type
참조형은 메모리 주소로 값에 접근하는 타입이다.
- *Integer*, *String*, *Boolean* ... *array*...  *enum*, *class* , *interface* ...

여기서 의문이 들 수 있다. 왜 *int*는 원시타입인데 *Integer*는 참조타입인가??
*Integer* 클래스를 확인 해 보자. *Integer*는 단순 값 타입이 아닌, 클래스이다. 따라서 참조형인 것이다. *int*는 IDE에서 암만 꾹 눌러도, 클래스 정의 위치로 이동하지 않는다. 단순 값이기 때문에...
```java
@jdk.internal.ValueBased  
public final class Integer extends Number  
        implements Comparable<Integer>, Constable, ConstantDesc {
}
```

원시형에 반해 데이터 사이즈가 **가변적**이기 때문에, 값이 *Heap*에 저장된다.
## 차이점
1. 성능
원시타입을 다루는게 더 빠르다. ($\because$ *Stack*은 이미 할당되어 있는 공간을 사용하기 때문에, *Heap*보다 빠르기 때문)

2. NULL 여부
```java
int a = null; // 불가능
```

```java
Integer a = null; // 가능
```

## 유의사항

원시타입은 값만 복사되기 때문에 아래와 같은 코드가 예상대로 흘러간다.
```java
// primitive type
int a = 1;  
int b = a;  
b = 10;  
  
System.out.println("a : " + a);  
System.out.println("b : " + b);
```

```
a : 1
b : 10
```

하지만 참조타입은 객체의 Reference 주소가 복사되기 때문에, `sb2`를 수정했음에도 `sb1`에 영향이 간다.
```java
// reference type  
StringBuilder sb1 = new StringBuilder("test");  
StringBuilder sb2 = sb1;  
sb2.append("append sb2");  
System.out.println("sb1 : " + sb1.toString());  
System.out.println("sb2 : " + sb2.toString());
```

```java
sb1 : testappend sb2
sb2 : testappend sb2
```

따라서 값을 복사할때 내 의도대로 동작할 수 있도록 유의하여야 한다.