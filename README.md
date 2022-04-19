# 스프링 DB 1편 - 데이터 접근 핵심 원리

## 1. JDBC 이해
### `JDBC` 가 등장한 이유   
JDBC 표준 인터페이스(Connection, Statement, ResultSet)을 정의

>`java.sql.Connection` - 연결
>`java.sql.Statement` - SQL을 담은 내용
>`java.sql.ResultSet` - SQL요청 응답

개발자는 다른 종류의 데이터베이스로 변경하더라도 표준 인터페이스만 사용해서 개발하면 됨

표준화의 한계   
> 각각의 데이터베이스 마다 SQL, 데이터타입 등의 일부 사용법이 달라 데이터베이스 변경 시 JDBC 코드는 변경하지 않더라도
> SQL은 해당 데이터베이스에 맞도록 변경해야함.

### SQL Mapper vs ORM
- `SQL Mapper` : SQL만 작성하면 되지만 SQL을 직접 작성해야함
- `ORM` : SQL을 직접 작성하지 않고 ORM 기술이 SQL 을 대신 동적으로 만들어 실행

> 어떤 기술을 사용하더라도 내부에서는 모두 JDBC를 사용하기 때문에 해당 기술들을 깊이있게 이해하기 위해서는
> JDBC가 어떻게 동작하는지 기본 원리를 알아두어야 함

### 데이터베이스 연결
- JDBC가 제공하는 `DriverManager`가 라이브러리에 등록된 DB 드라이버들을 관리하고 커넥션을 획득하는 기능을 제공

- JDBC를 사용한 CRUD는 `MemberRepositoryV0` 코드 참조

## 2. 커넥션풀과 데이터소스 이해

### 커넥션 풀 이해
- 데이터베이스 커넥션을 매번 새로 만드는 것은 시간이 많이 소모되는 일이다.
- 커넥션을 미리 생성해두고 풀로 관리하는 것이 커넥션 풀
- 커넥션을 요청시 풀에서 이미 생성되어 있는 커넥션을 획득하고 사용을 다하면 반환함.
- 대부분 `HikariCP` 사용

### DataSource 이해
- 커넥션을 획득하는 방법을 추상화 하는 인터페이스
- `MemberRepositoryV1` 코드 참조

## 3. 트랜잭션 이해
