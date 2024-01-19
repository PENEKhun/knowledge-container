
관련 문서
- [equals 와 =\=의 차이](equals%20와%20==의%20차이.md)
# equals
가끔 JPA에서 엔티티를 비교할때 내가 원했던 기대값에서 벗어난 경우가 있다.
```java
TestEntity test1 = em.find(TestEntity.class, 1L);  
em.clear();  
TestEntity test2 = em.find(TestEntity.class, 1L);  
  
assert test1.equals(test2);
```
위 테스트는 실패됐다. 왜냐하면 `em.clear()`를 통해 영속성 컨텍스트를 비웠기 때문에, JPA에선 test1과 test2의 동일성(=\=)을 보장할 수 없기 때문이다. 

# hashcode

