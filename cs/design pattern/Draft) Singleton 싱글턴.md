객체 인스턴스를 한개만 만들어 사용할 때 이용하는 디자인패턴이다.

## 가장 기초적인 구현
```java
public class UserConfigurationLoader {

  private static UserConfiguration config;

  public static UserConfiguration getInstance() {
    if (config == null) {
      config = new UserConfiguration();
    }
    return config;
  }
}
```

`getInstance()`가 호출될 때 초기화를 하고 객체를 넘겨준다.