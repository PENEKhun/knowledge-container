
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


INSERT INTO join_test.Employee (id, name, departmentId) VALUES (1, '문성훈', 1);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (2, '김현수', 5);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (3, '허태영', 2);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (4, '송훈석', 2);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (5, '조수호', 4);
INSERT INTO join_test.Employee (id, name, departmentId) VALUES (6, '정지용', NULL);
```

</details>



#SQL #조인쿼리