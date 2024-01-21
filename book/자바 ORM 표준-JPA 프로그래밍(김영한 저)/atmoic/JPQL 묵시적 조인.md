`JPQL`에서 **명시적 조인**은 `JOIN`을 직접 적어주는 것이다.
```sql
SELECT m
FROM Member m JOIN m.team t
```
^96d82f
# JPQL의 묵시적 조인
[명시적 조인](#^96d82f)과 반대로 `join` 없이 **경로 표현식**(`a.b`)를 통해 조인을 할 수 있다.
```sql
SELECT m.team
FROM Member m
```

**경로 탐색을 이용한 묵시적 조인 시 주의 사항**
- 항상 내부 조인이다.
- 컬렉션은 경로 탐색의 끝이다. 컬렉션에서 경로 탐색을 하려면 명시적으로 조인해서 별칭을 얻어야 한다.
  - 가능한 케이스
```sql
SELECT t.members  
FROM Team t  
JOIN t.members m  
WHERE m.name = 'LG 1번째 팀원' 
```
  - 불가능한 케이스
```sql
SELECT t.members  
FROM Team t  
WHERE t.members.name = '홍길동' -- .name 에서 오류가 뜸
```