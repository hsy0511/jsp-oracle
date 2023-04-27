# jsp-oracle
# jsp 기초문법
## 1. jsp(Java Server Pages)란?
jsp는 기본적으로 html에서 자바코드를 넣어 실행된다.

그래서 사용할 때 대부분 변수 선언, 메서드 선언, 로직(논리)등은 자바 언어로 사용한다.

하지만 자바 코드를 html에서 사용할 때 필요한 문법이 있다.
## 2. jsp 스크릿틀릿
스크릿틀릿은 <% %>로 사용하는 태그이고, jsp 문법에서 가장 기초적인 태그이다.

대부분 jsp 문법을 스크릿틀릿을 기본으로 쓴다. 

```jsp
<% // 스크릿틀릿  %>
<% int a = 5; %>
<% int b = 5; %>
<% if(5>1){
	System.out.println("5는 1보다 크다");
}%>
```
## 3. jsp 선언부
선언부는 <%! %>로 사용하고 변수,메소드 등을 선언할때 사용하는 태그

```jsp
<% // 선언부 %>
<%! String name = "홍길동"; %>
<%! public int plus(int a, int b){ return a+b;} %>
```
## 4. jsp 표현부
표현부는 <%= %>로 사용되고 스크릿틀릿과 선언부에서 사용한 문법의 결과를 표현한다.

```jsp
<% // 표현부 %>
<p><%= name %></p>
<p><%= plus(5,5) %></p>
```
## 5. jsp 지시어
jsp 지시문은 서블릿 (동적 웹 페이지를 만들 때 사용되는 자바 기반의 웹 애플리케이션 프로그래밍 기술) 클래스의 전체 구조에 영향을 준고,

jsp 파일을 어떻게 처리할지 정보 등을 기술한다.

![image](https://user-images.githubusercontent.com/104752580/234434624-21757533-7f6f-4096-8901-dad898ce8393.png)

지시어에는 page, include, taglib 등이 있는데, 여기서 우리가 가장 많이 사용하는 page와 include를 알아보자.
## 5-1. 지시어 page
지시어 page는 jsp 엔진에게 jsp 파일에 대한 정보를 알려주는 역할을 한다.

page 속성을 알아보자.

![image](https://user-images.githubusercontent.com/104752580/234434990-038c31a6-6f83-4fa7-be68-28da6ff864df.png)

page 속성은 이러한 것들이 있다. 하지만 우리가 대표적으로 사용하는 속성 3개만 알아보자.

### 첫번째는 contentType이다.
contentType은 jsp 페이지가 생성할 문서의 타입을 지정하는 것이다.

예제를 보며 살펴보자.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

여기서 contentType이 text/html 이므로 html 문서 타입으로 페이지를 작성하겠다는 내용이 된다.
#### ※ utf-8 (Unicode Transformation Format - 8bit) : 가변 길이 유니코드 인코딩
### 두번째는 improt이다.
import는 jsp 페이지에서 자바의 클래스를 사용하기 위해서 사용하는 것이다.

예제를 보며 살펴보자.

```jsp
<%@ page import="java.sql.*" %>
```

여기서 import는 java sql 클래스를 사용하기 위해서 임폴트한 것이다.

### 세번째는 pageEncoding이다.
pageEncoding은 jsp 파일 작성시의 문자코드를 지정하기 위한 속성이다.

예제를 보며 살펴보자

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

여기서 pageEncoding을 utf-8로 지정했기 때문에 문서코드가 한글로 지정된 것으로 볼 수 있다. 

만약 여기서 utf-8이 아니고 ms949로 지정하게 되면 웹 페이지에서 한글이 글자깨짐 현상이 일어난다.

## 5-2. 지시어 include
지시어 include는 가져올 파일의 경로를 넣어 다른 파일을 가져와 현재 파일에 뿌려주는 역할을 한다.

바로 예제를 살펴보자

![image](https://user-images.githubusercontent.com/104752580/234438355-0d60fe06-28c7-4b46-95b4-4327e86c06b3.png)

같은 폴더에 두개의 jsp 파일을 만들었다.

![image](https://user-images.githubusercontent.com/104752580/234438425-ee587995-72ac-495e-b332-e0c66f7279eb.png)

ex1.jsp 파일에 <%@ include file="ex.jsp" %>를 하며 ex1.jsp 파일에 ex.jsp 파일을 뿌려넣은 것이다.

## 6. jsp 액션태그 
액션태그는 jsp 문서에서 간다하게 다양한 구현을 할 수 있도록 만든 태그이다.

액션태그를 알아보자.

![image](https://user-images.githubusercontent.com/104752580/234439886-22ab2d91-e934-4960-a2f7-9859dcf47bba.png)

액션태그에는 이러한 것들이 있다. 하지만 우리가 대표적으로 사용하는 태그 2개만 알아보자.

### 첫번째는 jsp:include이다. 

앞서 설명했던 include file과 비슷한 기능을 가지고 있다.

예제를 보며 살펴보자

![image](https://user-images.githubusercontent.com/104752580/234440457-9fa4cccd-f3be-48e1-b4e0-1b32a47c1f88.png)

같은 폴더 안에 두개에 페이지을 만들었다.

![image](https://user-images.githubusercontent.com/104752580/234440498-1b78d527-4074-44e0-8c91-f546082bcadc.png)

ex1.jsp 페이지에 <jsp:include page="ex.jsp">를 사용하여 ex1.jsp 페이지에 ex.jsp 페이지를 포함한 것이다.

### 두번째는 jsp:forward이다.

jsp:forward는 현재 페이지에서 다른 페이지로 이동할 때 사용하는 태그이다.

예제를 보며 살펴보자

![image](https://user-images.githubusercontent.com/104752580/234441165-5a2444fe-303d-44cf-bc07-a704a8812d63.png)

같은 폴더 안에 두개에 페이지을 만들었다.

![image](https://user-images.githubusercontent.com/104752580/234441270-41c0d0f0-fda1-4deb-bf3b-81e89e9225c8.png)

ex1.jsp 페이지에 <jsp:include page="ex.jsp">를 사용하여 ex1.jsp 페이지에서 ex.jsp 페이지로 이동한 것이다.

# oracle database 기초문법
oracle database는 크게 DQL, DDL, DML, DCL, TCL으로 4가지 그룹으로 나눌 수 있다.

## sql 실행순서
![image](https://user-images.githubusercontent.com/104752580/234499466-4388a46a-0032-4318-8d55-b2161f7ebe62.png)

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
alter table EX add ho varchar2(20); 추가
alter table EX modify column star bigint default 10000; 변경
alter table Ex drop column star, drop primary key; 삭제
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

EX 테이블에서 gno가 #**nn이면 #학년 **반으로 데이터를 조회한다.
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

