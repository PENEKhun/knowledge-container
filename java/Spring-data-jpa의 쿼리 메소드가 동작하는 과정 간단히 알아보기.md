# TL; DR
Spring Data JPA를 사용하면, `Repository` 인터페이스에 쿼리 메소드를 정의함으로써 복잡한 쿼리도 손쉽게 생성할 수 있습니다. 이 과정에서 Spring은 동적 프록시를 사용하여 실제 데이터베이스 쿼리를 생성하고 실행합니다. 여기서 중요한 역할을 하는 것이 [PartTree] 객체입니다. [PartTree]는 메소드 이름을 분석하여, 해당 메소드가 어떤 쿼리를 나타내는지 이해하는 데 사용됩니다. 

[PartTree]: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/query/parser/PartTree.html

예를 들어, `findByPriceGreaterThan` 메소드는 '가격이 특정 값보다 큰 주문을 찾아라'라는 쿼리를 나타냅니다. Spring Data JPA는 이 메소드 이름을 분석하여, `PartTree` 객체를 생성하고, 이를 바탕으로 JPQL 쿼리를 동적으로 생성합니다. 이 과정은 런타임에 이루어지며, 생성된 구문 해석(`PartTree`)은 캐싱되어 매 번 `Reflection`하여 메소드명을 해석할 필요 없이 효율적인 실행을 보장합니다.
# Introduction
> spring-data-jpa-3.2.1 기준

```java
public interface OrderRepository extends JpaRepository<Order, Long> {   
  List<Order> findByPriceGreaterThan(int price);  
  
}
```

`Spring-data-jpa`를 이용하면 `Repository` 인터페이스를 생성하고 메서드를 정의하는 것만으로도 자동으로 쿼리가 실행됩니다. 이러한 `Repository`는 인터페이스이며, 메서드를 별도로 구현하지 않았음에도 불구하고 어떻게 동작하는 것일까요?

이에 대한 완벽한 이해와 자세한 설명은 아니지만, 그 과정을 디버깅을 통해 간략하게 정리해보고자 합니다.
# Body
다음 코드를 BreakPoint 설정 후 스텝인투를 해보자.
```java
orderRepository.findByPriceGreaterThan(50000);
```

`orderRepository`에 주입된 객체는 프록시임을 확인 할 수 있었다.
![](repo-is-proxy.png)

Spring Data JPA는 개발자가 메소드를 구현하지 않아도, **다이나믹 프록시**를 통해 자동으로 쿼리를 실행하는 구현체를 생성합니다.
*(보다 자세한 내용은 [프록시 패턴](프록시%20패턴.md)을 참고)*

```java
MethodInvocation invocation = new ReflectiveMethodInvocation(proxy, target, method, args, targetClass, chain);  
retVal = invocation.proceed(); //여기서 쿼리를 실행
```

이제 프록시를 `Intercept`하는 부분을 찾아가며 더 자세히 추적해보겠습니다.
그러던 중 `QueryExecutorMethodInterceptor`를 발견했습니다.

```java
// QueryExecutorMethodInterceptor.java
private Object doInvoke(MethodInvocation invocation) throws Throwable {  
  Method method = invocation.getMethod();  
  if (this.hasQueryFor(method)) {  
    RepositoryMethodInvoker invocationMetadata = (RepositoryMethodInvoker)this.invocationMetadataCache.get(method);  
    if (invocationMetadata == null) { // 메타데이터 존재 여부 확인
      invocationMetadata = RepositoryMethodInvoker.forRepositoryQuery(method, (RepositoryQuery)this.queries.get(method));  
      this.invocationMetadataCache.put(method, invocationMetadata);  
    }

// ... 후략
```
여기서 실행할 구문에 대한 `Metadata`가 없다면, 해당 메서드 이름을 해석하고 캐싱합니다.

![](Pasted%20image%2020240216224509.png)
위 그림을 보면, 쿼리 메소드(`findByPriceGreaterThan(int price)`)에 대한 구문 해석이 저장되어 있습니다. 이 과정은 `Reflection`을 통한 쿼리 메소드의 재해석 과정을 생략 하므로, 실행 시간을 단축시키는 역할을 합니다.

마지막으로, 메소드 이름이 해석된 `PartTree` 객체가 실제 쿼리로 변환되는 시점을 확인하면 됩니다. `PartTreeJpaQuery`에는 `doCreateQuery()` 메소드가 있습니다.

```java
public Query doCreateQuery(JpaParametersParameterAccessor accessor) {  
  return this.query.createQuery(accessor);  
}
```

이 메소드에서 메서드 이름이 쿼리로 변환됩니다.
# Conclusion
기존에 저는 어노테이션 프로세싱을 통해 컴파일 시점에 쿼리가 '일부' 작성된다고 생각 했었습니다. 하지만 실제로는 런타임에 쿼리 메소드가 호출될 때 `Reflection`과 `Dynamic Proxy`를 통해 해석이 시작되는 것이었습니다.