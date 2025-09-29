# SQL - BE
## 1) SQL이란?
### Structured Query Language
- SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있도록 고안된 컴퓨터 언어이다.
- 관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단이다.
- DML (Data Manipulation Language) : 데이터를 조작하기 위해 사용한다.
  - INSERT, UPDATE, DELETE, SELECT 등이 여기에 해당한다
- DDL (Data Definition Language) : 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용한다.
  - CREATE, DROP, ALTER 등이 여기에 해당한다.
- DCL (Data Control Language) : 데이터를 제어하는 언어이다. 권한을 관리하고 데이터의 보안, 무결성 등을 정의한다.
  - GRANT, REVOKE 등이 여기에 해당한다.
### Database 생성하기
- 콘솔에서 mysql -uroot -p 를 실행해서 관리자 계정인 root로 dbms에 접속하겠다는 뜻
- mysql> create database DB이름; 으로 데이터베이스 생성
- connectdb 라는 이름을 가진 데이터베이스 생성
### Database 사용자 생성과 권한 주기
- 데이터베이스를 사용하는 계정 생성 필요
- 해당 계정이 데이터베이스를 이용할 수 있는 권한을 줘야 함
- db 이름 뒤의 *는 모든 권한을 의미한다
- @'%'는 어떤 클라이언트에서든 접근가능하다는 의미
- @'localhost'는 해당 컴퓨터에서만 접근가능하다는 의미이다
- fulsh privileges는 DBMS에 적용하라는 의미. 반드시 실행해줘야 한다.
- grant all privileges on db이름.* to 계정이름@'%' identified by '암호';
- grant all privileges on db이름.* to 계정이름@'localhost' identified by '암호';
- flush privileges;
- 사용자 계정이름은 connectuser, 암호는 connect123!@# 으로 생성
### 생성한 databse에 접속하기
- mysql -h호스트명 -uDB계정명 -p 데이터베이스이름
- 위 명령을 실행하여 원하는 데이터베이스에 접속할 수 있다.
- db 이름이 connectdb, db계정이 connectuser, 암호가 connect123!@#일 경우 콘솔창에서 다음과 같이 입력한다.
- mysql -h127.0.0.1 -uconnectuser -p connectdb [enter]
- quit;을 통해 종료 가능
- select version(), current_date; 를 통해 현재 버전과 최근 실행날짜를 알 수 있다.
- 키워드는 대소문자를 구별하지 않는다.
- show databases; 를 통해 database목록 확인가능
- use db명; 을 통해 database 선택 가능
### 테이블의 구성 요소
- 테이블 : RDBMS의 기본적인 저장구조 - 한개 이상의 column과 0개 이상의 row로 구성
- 열(Column) : 테이블 상에서의 단일 종류의 데이터를 나타냄. 특정 데이터 타입 및 크기를 가지고 있음
- 행(Row) : Column들의 값의 조합. 레코드라고도 불린다. 기본키(PK)에 의해 구분된다.
- Field : Row 와 Column의 교차점으로 데이터를 포함할 수 있고 없을 때는 null값을 가지고 있다.