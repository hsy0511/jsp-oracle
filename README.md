# oracle
# oracle database 기초문법
oracle database는 크게 DQL, DDL, DML, DCL, TCL으로 5가지 그룹으로 나눌 수 있다.

## sql 실행순서
![image](https://user-images.githubusercontent.com/104752580/234499466-4388a46a-0032-4318-8d55-b2161f7ebe62.png)

sql은 from -> where -> group by -> having -> select -> orderby 순으로 실행된다.

## DQL
DQL은 데이터 질의(의심나는 점을 물어서 밝히는 것) 언어이다.

DQL에는 select가 있다. select는 DML에도 사용 가능하다.

select 사용 방법은 DML에서 설명 하겠다.
## DDL (Data Definition Language)
DDL은 DB에서 데이터를 정의하는 언어이다. (생성, 수정, 삭제가 가능한 명령어)

DDL은 크게 create, drop, alter 등으로 나뉜다.

### CREATE
create는 테이블을 생성한다.

```sql
EX 테이블을 생성한다.
create table EX( 
gno number(5) not null primary key,
school varchar2(40),
name varchar2(20),
phone varchar2(30)
);
```
### DROP
drop은 테이블을 삭제한다.

```sql
EX 테이블을 삭제한다.
drop table EX;
```

### ARTER
alter는 테이블의 데이터를 추가, 변경, 삭제한다.

```sql
EX 테이블 내용을 추가, 변경, 삭제한다.
alter table EX add ho varchar2(20); ho 컬럼 추가
alter table EX modify column star bigint default 10000; star 컬럼에 기본 데이터 값을 100으로 변경
alter table Ex drop column star, drop primary key; 제약조건 기본키 삭제
```

DDL에서 자주 사용되는 데이터 타입을 알아보자

DDL에서 자주 사용되는 데이터 타입으로는 char, varchar2, date, number 등이 있다.

- char는 고정길이(레코드의 길이를 일정하게 지정해놓는 방법) 문자형을 저장한다.

- varchar2는 가변길이(필요한 만큼의 저장 공간만 차지하여 저장되는 문자의 개수) 문자형을 저장한다.

- date는 날짜, 연도, 월, 일, 시간 등을 저장한다.

- number는 숫자형을 저장한다.(음수, 양수)
## DML (Data manipulation language)
DML은 DB에서 데이터를 조작하는 명령어이다. (데이터 조회, 삽입, 변경, 삭제 가능한 명령어)

DML은 크게 select, insert, update, delete 등으로 나뉜다.

### SELECT
select는 데이터를 조건 값에 따라서 조회한다.

```sql
EX 테이블의 모든 데이터를 조회한다.
select * from EX;

EX 테이블의 school 데이터를 조회한다.
select school from EX;

EX 테이블에서 school 데이터가 성일정보고인 모든 데이터를 조회한다.
select * from EX
where
school = '성일정보고';

EX 테이블에서 school 데이터가 성일정보고인 name 데이터를 조회한다.
select name from EX
where
school = '성일정보고';

EX 테이블에서 gno가 31528이면 3학년 15반으로 데이터를 조회한다.
select case gno
when 31528 then '3학년 15반'
when 30212 then '3학년 2반'
when 30802 then '3학년 8반'
when 31111 then '3한년 11반'
end as gno
from ex;

EX 테이블에서 EZ 테이블에 name으로 조인한 값에 jno와 food 데이터를 조회한다.
select x.name, z.jno, z.food from ex x, ez z
where x.name = z.name;
```

### INSERT
insert는 데이터를 삽입한다.

```sql
EX 테이블에 데이터를 삽입한다.
insert into EX values(31528,'성일정보고','허성영','010-7736-7452');
insert into EX values(30212,'성일고','허성일','010-7736-7452');
insert into EX values(30802,'풍생고','허성이','010-7736-7452');
insert into EX values(31111,'성일정보고','허성삼','010-7736-7452');
```

### UPDATE
update는 데이터를 변경한다.

```sql
EX 테이블에서 name이 허성함인 phone 데이터를 변경한다.
update EX set phone = '010-7736-7452'
where name = '허성삼';
```

### DELETE
delete는 데이터를 조건 값에 따라서 삭제한다.

```sql
EX 테이블에 있는 모든 데이터 삭제
delete from EX;

EX 테이블에서 name이 허성삼인 데이터 삭제
delete from EX where name = '허성삼';
```

## DCL (Data Control Language)
DCL은 DB에서 데이터에 대한 객체 권한 부여 등의 제어어이다.

DCL은 크게 grant, revoke 등으로 나뉜다.

### GRANT
grant는 사용자에게 시스템 접속 권한을 부여하거나, 생성, 병경, 추가, 삭제 권한을 부여한다.

```sql
grant create user, alter user, drop user to scott with admin option;
```

SCOTT 계정에서 데이터를 CREATE, ALTER, DROP 할 수 있게 권한을 준다.

### REVOKE
revoke는 grant로 사용자에게 부여한 권한을 삭제한다.

```sql
revoke create user, alter user, drop user from scott;
```

SCOTT 계정에 준 권한을 삭제한다.
## TCL (Transaction Control Language)
TCL은 DB에서 트랜잭션을 제어하는 명령어이다.(데이터를 저장하여 복구 가능한 명령어)

※ 트랜잭션 : 쪼갤 수 없는 업무 처리의 최소 단위

TCL은 크게 commit, rollback, savepoint 등으로 나뉜다.

### COMMIT
commit은 이전 데이터를 영구히 저장하기 위해 쓰인다.

![image](https://user-images.githubusercontent.com/104752580/234478079-3f0adc4d-2e7e-4102-b7f3-fad3c3527aee.png)

commit으로 테이블을 조회 할 때 까지를 저장한다.

### ROLLBACK
rollback은 이전 commit까지 데이터를  복구 시킨다.

![image](https://user-images.githubusercontent.com/104752580/234477238-3f94c3fc-a81d-4070-a431-883ab7f243fc.png)

테이블을 삭제하기 전 commit까지 복구 시킨다.

### SAVEPOINT
savepoint도 commit과 같이 사용하지만 다른점은 지점을 저장한다.
즉, commit과 rollback을 사용하면 바로 이전 commit까지 데이터를 복구하지만
savepoint는 지정한 c1값까지 데이터를 복구한다. rollback to savepoint c1을 사용한다.

![image](https://user-images.githubusercontent.com/104752580/234477614-c9ce777c-8366-4bfc-aa1d-22f9af3e5e1d.png)
![image](https://user-images.githubusercontent.com/104752580/234477647-3b08c5d5-5e16-448c-88bc-17f7df71271f.png)

