
# 예시 테이블

## Employee Table
| name | departmentID |
| ---- | ---- |
| 문성훈 | 1 |
| 김현수 | 5 |
| 허태영 | 2 |
| 송훈석 | 2 |
| 조수호 | 4 |
| 정지용 | 4 |
## Department Table 

| departmentID | name |
| ---- | ---- |
| 1 | 소프트웨어개발팀 |
| 2 | 보안연구팀 |
| 3 | 경호팀 |
| 4 | 스팀 |
| 5 | 보안파견팀 |

### DDL/ DML
```sql
create table Department  
(  
    id             int auto_increment  
        primary key,    departmentName varchar(10) null comment '부서명'  
)  
    comment '부서 테이블';  
  
create table Employee  
(  
    id           int auto_increment  
        primary key,    name         varchar(10) null comment '직원이름',  
    departmentId int         null comment '부서 id');
```