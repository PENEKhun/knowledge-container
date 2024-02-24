# 예시 테이블
다음 예시 데이터들을 확인하여, 아래에 있을 실습에 착오가 없길 바란다.
## Employee Table
| name | departmentID |
| ---- | ---- |
| 문성훈 | 1 |
| 김현수 | 5 |
| 허태영 | 2 |
| 송훈석 | 2 |
| 조수호 | 4 |
| 정지용 | `NULL` |
## Department Table 
| departmentID | name |
| ---- | ---- |
| 1 | 소프트웨어개발팀 |
| 2 | 보안연구팀 |
| 3 | 경호팀 |
| 4 | 스팀 |
| 5 | 보안파견팀 |
| 6 |  |
<details>
<summary>예제 SQL 확인(DDL/DML)</summary>


MySQL로 작성되었음.

```mysql
create table Department
(
    id             int auto_increment
        primary key,
    departmentName varchar(10) null comment '부서명'
)
    comment '부서 테이블';


create table Employee
(
    id           int auto_increment
        primary key,
    name         varchar(10) null comment '직원이름',
    departmentId int         null comment '부서 id'
);

INSERT INTO join_test.Department (id, departmentName) VALUES (1, '소프트웨어개발팀');
INSERT INTO join_test.Department (id, departmentName) VALUES (2, '보안연구팀');
INSERT INTO join_test.Department (id, departmentName) VALUES (3, '경호팀');
INSERT INTO join_test.Department (id, departmentName) VALUES (4, '스팀');
INSERT INTO join_test.Department (id, departmentName) VALUES (5, '보안파견팀');
INSERT INTO join_test.Department (id, departmentName) VALUES (6, NULL);


INSERT INTO join_test.Employee (id, name, departmentId) VALUES (1, '문성훈', 1);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (2, '김현수', 5);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (3, '허태영', 2);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (4, '송훈석', 2);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (5, '조수호', 4);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (6, '정지용', NULL);
```

</details>

# SQL Join
SQL에서 Join은 크게 두가지가 있다.
## Inner Join
![200x200](innerjoin-visualize.png)
**Inner Join**은 두 집합에서 공통적으로 포함하고 있는 부분만 조인하는 방식이다.  
따라서 두 테이블에서 연관된 *ROW*들만 결과로 출력된다.
### 실습
사용법 : **inner Join 혹은 Join을 From절 이후에 추가**하면 된다.
```sql
SELECT  
  e.NAME,  
  d.departmentname  
FROM  
  Employee e  
  INNER JOIN Department d ON d.id = e.departmentId; -- 이렇게 !
```

[[SQL의 조인#Employee Table]]을 확인해보면 정지용의 부서ID 가 NULL임을 확인 할 수 있다.
*Inner Join* 은 두 관계에서 연관된 데이터만 가져오므로, 실행결과에 부서 *ID* 가 없는 *(== 부서 테이블과 연관 없는)* 정지용 직원 *ROW* 는 포함되지 않는다.

| name | departmentName |
| ---- | ---- |
| 문성훈 | 소프트웨어개발팀 |
| 김현수 | 보안파견팀 |
| 허태영 | 보안연구팀 |
| 송훈석 | 보안연구팀 |
| 조수호 | 스팀 |

- 연상법 :
	두 원이 있고, Inner니깐 안이 채워짐 => 교집합
## Outer Join
교집합이었던 [[SQL의 조인#Inner Join]] 과 달리 Outer Join은 합집합을 의미한다.
~~Outer Join을 그림으로 나타내면 좀 다양하지만... 대표적인 것 3가지만 그려보았다.~~
![350x350](outerjoin-visualize.png)

**`Join` 다음 명시해주는 테이블이 그림에서 의미하는 B 라고 생각하면 된다.**

- 연상법 :
	두 원이 있고, Outer니깐 바깥쪽 색이 칠해짐 => `합집합`
### Left Outer Join
> $A\cup B$ 의 결과를 $A$ 기준으로 표현하는 것이다.

$Employee \cup Department$ 를 **Employee** 기준으로 표현하게되면, **Department**를 가지지 않는 사람들도 실행 결과에 나타낼 수 있다.
#### 실습
```mysql
SELECT  
  e.NAME,  
  d.departmentname  
FROM  
  Employee e  
  LEFT OUTER JOIN Department d ON d.id = e.departmentId; -- 이렇게 !
```

결과 :

| name | departmentName |
| ---- | ---- |
| 문성훈 | 소프트웨어개발팀 |
| 김현수 | 보안파견팀 |
| 허태영 | 보안연구팀 |
| 송훈석 | 보안연구팀 |
| 조수호 | 스팀 |
| 정지용 | `null` |
부서 정보를 가지지않은 정지용도 검색되었다.
### Right Outer Join
> $A\cup B$ 의 결과를 $B$ 기준으로 표현하는 것이다.
#### 실습
[[SQL의 조인#Left Outer Join]] 아까 예시에서 A, B를 바꾸고 Right Join으로 실습을 진행했다.

```mysql
SELECT  
    e.NAME,    
	d.departmentname
FROM
    Department d -- 변경
    RIGHT JOIN Employee e ON d.id = e.departmentId; -- 변경
```

결과도 이전 실습과 똑같다 :

| name | departmentName |
| ---- | ---- |
| 문성훈 | 소프트웨어개발팀 |
| 김현수 | 보안파견팀 |
| 허태영 | 보안연구팀 |
| 송훈석 | 보안연구팀 |
| 조수호 | 스팀 |
| 정지용 | `null` |
### Full outer join
두개의 테이블의 합집합이다. MySQL에선 지원하지 않는다.
MySQL에서 사용하려면, Left join과 Right join 각 쿼리를 합쳐서 사용해야한다.  
쿼리간 결과를 합칠땐 #UNION 을 사용한다.

```sql
SELECT  
    *  
FROM  
    Employee e  
LEFT OUTER JOIN Department d on d.id = e.departmentId  
UNION -- 여기  
SELECT  
    *  
FROM  
    Employee e  
RIGHT OUTER JOIN Department d on d.id = e.departmentId
```

실행결과 : 

| id | name | departmentId | id | departmentName |  
| :--- | :--- | :--- | :--- | :--- |  
| 1 | 문성훈 | 1 | 1 | 소프트웨어개발팀 |  
| 2 | 김현수 | 5 | 5 | 보안파견팀 |  
| 3 | 허태영 | 2 | 2 | 보안연구팀 |  
| 4 | 송훈석 | 2 | 2 | 보안연구팀 |  
| 5 | 조수호 | 4 | 4 | 스팀 |  
| 6 | 정지용 | null | null | null |  
| null | null | null | 3 | 경호팀 |


#MySQL #SQL #조인쿼리