JAVA에서는 `obj.equals()`와 `obj1 == obj2` 이 두가지를 통해 객체를 비교한다.
과연 이 둘은 무슨 차이가 있을까?

흔히 `equals()`는 값을 비교한다하고, `==`는 주소값을 비교한다고 한다.

바로 코드로 작성해보자.
```java
String str1 = new String("Hello");  
String str2 = new String("Hello");  
String str3 = str1;  
  
// equals 메서드를 사용하여 값 비교  
System.out.println("str1.equals(str2): " + str1.equals(str2));  
System.out.println("str1.equals(str3): " + str1.equals(str3));  
  
// == 연산자를 사용하여 주소 비교  
System.out.println("str1 == str2: " + (str1 == str2));  
System.out.println("str1 == str3: " + (str1 == str3));
```

위 코드의 결과 값 :
```java
str1.equals(str2): true
str1.equals(str3): true
str1 == str2: false
str1 == str3: true
```

`str1`, `str2`, `str3` 모두 **Hello**라는 값을 가지고 있어 `.equals()`는 `참`을 반환한다.
하지만 `==`는 주소를 비교하기 때문에 `str1 == str2`는 `거짓`을 반환한다.


관련 문서
- [equals와 hashcode를 오버라이딩하는 이유](equals와%20hashcode를%20오버라이딩하는%20이유.md)

