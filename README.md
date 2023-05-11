# oracle-foundation
# oracle database 기초문법
oracle database는 크게 DQL, DDL, DML, DCL, TCL으로 5가지 그룹으로 나눌 수 있다.

## sql 실행순서
![image](https://user-images.githubusercontent.com/104752580/234499466-4388a46a-0032-4318-8d55-b2161f7ebe62.png)

### sql은 from -> where -> group by -> having -> select -> orderby 순으로 실행된다.

![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/e7af957d-13bf-4e09-9d2c-5f09fe6fcb9e)
###### ※ 레코드: 데이터베이스에서 하나의 단위로 취급되는 자료의 집합
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

DDL에서 사용되는 데이터 타입을 알아보자
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/26f2d034-1b1b-4682-90c9-6ed79baaf94a)
###### ※ 유니코드: 전 세계의 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준방식
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/e0f55faf-546a-4282-b52c-cfc9a38c6af5)
###### ※ 부동소수점: 소수점의 위치를 고정하지 않고 그 위치를 나타내는 수를 따로 적는 소수점
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/946bffc7-6bd3-4f87-9034-b7acfe5bf974)
###### ※ BC: 기원전
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/44b8c8ca-4a99-47b5-98c3-e7267e70ff1c)
###### ※ lob: 대용량 데이터를 저장할 수 있는 데이터 타입(그래픽, 이미지, 사운드등 비정형 데이터)
###### ※ 문자집합: 정보를 표현하기 위한 글자나 기호들의 집합
DDL에서 자주 사용되는 데이터 타입은 char, varchar2, date, number 등이 있다.

- char는 고정길이(레코드의 길이를 일정하게 지정해놓는 방법) 문자형을 저장한다.

- varchar2는 가변길이(필요한 만큼의 저장 공간만 차지하여 저장되는 문자의 개수) 문자형을 저장한다.

- date는 날짜, 연도, 월, 일, 시간 등을 저장한다.

- number는 숫자형을 저장한다.(음수, 양수)

### char와 varchar2의 차이점
char는 고정길이고, varchr2는 가변길이이다.

즉, char는  CHAR(8)로 선언 시 글자를 한 개를 넣든 두 개를 넣든 8바이트의 공간을 차지합니다.

하지만 varchar2는 VARCHAR(8)로 선언 시 글자를 한 개를 넣으면 1바이트, 2개를 넣으면 2바이트의 공간을 유동적으로 차지합니다.
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
EX 테이블에서 name이 허성인 phone 데이터를 변경한다.
update EX set phone = '010-7736-7452'
where name = '허성삼';
```
### alter와 update 차이점
![image](https://github.com/hsy0511/oracle-/assets/104752580/b5b94b86-4ca7-4c83-8eed-e2a6e1f6034d)
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
막약에 saveponit를 사용할 때 c1, c2, c3가 있으면 c3를 갔다가 c1를 갈 수 있지만, c1을 간다음에 c2와 c3를 갈수는 없다.

![image](https://user-images.githubusercontent.com/104752580/234477614-c9ce777c-8366-4bfc-aa1d-22f9af3e5e1d.png)
![image](https://user-images.githubusercontent.com/104752580/234477647-3b08c5d5-5e16-448c-88bc-17f7df71271f.png)


## 서브쿼리
서브쿼리는 쿼리문을 작성할 때 메인쿼리 안에서 작성하는 쿼리이다.

서브쿼리에는 주로 3개에 서브 쿼리를 씁니다.

![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/98b9c716-a4ca-4290-bd61-f3032d603aae)
###### ※ 뷰: 관계 데이터베이스의 데이터베이스 언어 SQL에서 하나 이상의 테이블에서 원하는 모든 데이터를 선택하여, 그들을 사용자 정의하여 나타낸 것이다.
###### ※ 스칼라: 단일값에 적용이 되어서 단일값의 결과(즉, 여기서는 dept 테이블에서 dept_name 데이터를 가져온것이다.)
### 뷰와 인라인 뷰 차이점
뷰는 재활용이 가능하지만 인라인 뷰는 쿼리문에서만 사용되는 임시 뷰이기 때문에 재활용이 불가능 하다.
### 스칼라 서브 쿼리 예제
dept_name을 가져오는 쿼리입니다. 

스칼라 서브쿼리를 이용하여 select문 안에서 dept 테이블을 연결합니다.(아우터 조인을 대신하여 사용)

![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/07405bec-8652-4a18-b41b-036c6c251781)
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/f90da64c-17fd-4ab6-adf4-5ee2b7da0833)

### 인라인 뷰 예제
인라인 안에서 실행되는 쿼리문으로 from 절에서 사용되는데 예제에서는 inner join을 사용하여 dept 테이블과 연결 시켜주었다.

![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/3e9f5b7e-a443-4186-aaf2-293e9e447e62)
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/2402943b-ca97-4db8-a482-dc27e5377c8c)
### 중첩 서브쿼리 예제
중첩 서브쿼리는 서브쿼리를 중첩하여 사용할 수 있는 것으로 예제에서는 in으로 서브쿼리를 중첩하여 사용했다.

![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/a9f11bd0-d4e4-45ec-8919-9123e2dc7b17)

## 오라클에서 사용되는 명령어(위에서 설명한것 제외)
### 모든 테이블 출력
```sql
select * from tab;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/b4961415-a2bd-4a3e-be68-2bb2e7f219c3)
### 테이블 구조 확인
```sql
desc dept;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/cb2c3802-b067-4f07-bced-92efce36b942)
### 산술연산처리(숫자형 컬럼만 가능하다.)
```sql
select ename, sal*12 from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/2a2b18ef-41d7-4590-b054-e43f0b19d498)
### 별칭(alias)
```sql
select empno as num, ename as name from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/2abcaa92-cb0f-446d-9908-3b78da71055f)
```sql
select empno num, ename name from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/2abcaa92-cb0f-446d-9908-3b78da71055f)
```sql
select empno "<n u m>", ename "<n a m e>" from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/c145847f-7412-4a30-9ce2-abf8dff06f40)
```sql
select empno "<n u m>", sql*100 "$ S A L" from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/f15a6630-98d5-4cde-8926-d0987cc5ed6a)
### || 연결 연산자
###### ※ 주의할 점: 오라클에서 문자열은 (' ')로 표현된다.(" ")는 오직 별칭을 사용할 때만 사용된다. 
```sql
select ename, 'is a', job from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/d14b3ac4-f8f3-4af7-a643-fe5b17e93e34)
```sql
select ename || 'is a' || job from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/51513a33-fd59-4ae0-bfb2-b1887cf58d96)
### distinct(중복제거)
```sql
select deptno from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/b6439227-d9f2-46b7-b684-5e9fdfda9960)
```sql
select distinct deptno from emp;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/9d356d24-94f1-42b3-b056-841ede7ae6d5)
### like 연산자(해당 문자포함 여부)
- 이름이 J로 시작하는 사원
```sql
select ename from emp WHERE ename LIKE 'J%';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/5800fbfb-8963-4478-9290-a8a65bfdb0d2)

- 이름에 A가 들어가는 사원
```sql
select ename from emp WHERE ename LIKE '%A%';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/7abab802-fc68-483b-927b-75707b84ecdf)

- 이름이 N으로 끝나는 사원
```sql
select ename from emp WHERE ename LIKE '%N';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/812957bc-d10c-4867-b39f-3ae2ed62fc0f)

- 이름의 두 번째 글자가 A인 사원
```sql
select ename from emp WHERE ename LIKE '_A%';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/81cb3ec2-acfc-404a-9bd2-45895e2973ec)

### in 연산자
- 여러개의 값 중에서 일치하는 값이 있으면 참
- 두개말고 여러개도 가능 
- 논리 연산자 or 대신 사용 가능
- 날짜와 문자도 비교 가능
```sql
select empno, ename, deptno from emp where deptno in (10,20);
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/344e5a17-633f-44c6-9cd8-9d685c0a3a49)
```sql 
select empno, ename, job
from emp
where job in ('CLERK', 'MANAGER');
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/8e97024d-28e9-47df-b398-8865eeed1e4f)
### between a and b 연산자
- a에서 b까지의 범위 값을 조회
- 논리연산자 and 대신 사용 가능
```sql
select ename from emp where sal between 2000 and 4000;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/31714a5a-bbe8-4ba8-8d85-3419e7efd3d0)
### 논리 연산자(where 절에 조건이 두 개 이상일 경우)
- AND: 두 조건을 모두 만족
```sql
select ename, job, deptno from emp where job = 'CLERK' and deptno = 10;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/53828e70-b0c7-4e6b-a181-e2ec742e4ce9)
```sql
select ename, job, sal from emp where sal >= 2000 and sal <= 4000;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/f5fb0f31-5dcf-468f-9c75-63976dcf67fd)
- or: 두 조건 중에서 한 가지만 만족
```sql
select ename, job, deptno from emp where job = 'CLERK' or job = 'MANAGER';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/283ec258-5c29-49d8-ad4b-48ded5e6ff20)
```sql
select ename, job, deptno from emp where deptno = 10 or deptno = 20;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/f5ecf081-71e9-4190-b2f6-71663a710059)
### 논리 연산자(where 절의 조건에 해당하지 않을 경우 검색
- not
```sql
select empno, ename, deptno from emp where not deptno = 20;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/88954cf1-d389-4720-898e-64369a67006b)
- not in
```sql
select empno, ename, deptno from emp where deptno not in (10,20);
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/e9cd4e36-763e-40b5-8ff6-5be206e4c9e8)
- not between a and b
```sql
select empno, ename, sal from emp where sal not between 2000 and 4000;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/d2427412-dbe8-453e-97e0-8912a0f10d09)
- not like
```sql
select empno, ename from emp where ename not like '%A%';
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/dd36b80e-5346-4f19-8b4e-27f95dcbfbbd)
### is null, is not null(컬럼값이 null인지 아닌지 비교)
- null
```sql
select empno, ename, mgr from emp where mgr is null;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/a9725683-936b-4eae-9777-c8a58da9a2ca)
- is not null
```sql
select empno, ename, mgr from emp where mgr is not null;
```
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/cf0c167d-f1c0-4e24-918c-f3871a493416)
## oracle 단축키
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/93d7aa38-1d33-4ab0-8fd6-686a219719dc)
###### ※ 세션: SQL명령어 사용을 통해서 데이터베이스와의 상호 연결되어 있는 기간
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/3f230ed5-08c1-48a3-bdd4-50c07d9fdff2)
###### ※ 스크립트: 여러 쿼리문이 모여있는 것
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/bc096b18-72c2-47b0-9426-b15c1be954ae)
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/60930b29-ce2b-49b5-adc3-8a0fdca51d1e)
![image](https://github.com/hsy0511/oracle-foundation/assets/104752580/82b077c1-2d79-4c24-b3e9-2fc49a019532)
## oracle 특징
- 1. DB서버가 통합된 하나의 스토리를 공유하여 사용한다.
- 2. 별도의 DBMS를 설치해 사용하는 것이 불가능하다.
- 3. 메모리 사용율이 커서 최소 수백 MB를 요구한다.
- 4. Multiple Database 튜닝이 가능함(mupltiple: 다수의)
- 5. 다수의 사용자가 동시 접근이 가능하다.
- 6. 변경 plan을 작성하고 실제 구현 전의 변경 사향의 효과를 볼 수 있다. 
- 7. 유료화로 인한 비용부담
- 8. 많은 기능으로 초보자의 접근이 어려움
## oracle을 사용하는 이유
오라클 DB를 쓰는 가장 큰 이유는 RAC(Real application clusters)라는 기능 때문이다.

RAC는 간단히 말하면 하나의 DB를 여러 서버가 공유하는 기술이다.

그래서 하나의 DB를 여러 서버가 공유하기 때문에 서버 하나가 장애가 나도 데이터 정합성이 유지되기 때문이다.


