# 예시 테이블
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

```sql
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
Inner Join은 두 집합에서 공통적으로 포함하고 있는 부분만 조인하는 방식이다.
따라서 두 집합에서 빈 값(NULL)이 있으면 포함하지 않는다.
## 실습
사용법 : **inner Join 혹은 Join을 From절 이후에 추가**하면 된다.
```sql
SELECT  
  e.NAME,  
  d.departmentname  
FROM  
  Employee e  
  INNER JOIN Department d ON d.id = e.departmentId; -- 이렇게 !
```

[[SQL의 조인#예시 테이블#Employee Table]]을 확인해보면 정지용의 부서ID 가 NULL임을 확인 할 수 있다.
Inner Join은 빈 값은 포함시키지 않는다 했으니, 실행결과에 부서 ID가 없는 정지용 row는 포함되지 않는다.

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




#SQL #조인쿼리