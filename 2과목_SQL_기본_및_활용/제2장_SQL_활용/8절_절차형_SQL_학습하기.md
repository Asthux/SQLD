**절차형 SQL**

- 일반적인 개발 언어처럼 SQL에도 절차 지향적인 프로그램이 가능하도록 DBMS 벤더별로 PL(Procedural Language)/SQL(Oracle), SQL/PL(DB2), T-SQL(SQL Server) 등의 절차형 SQL을 제공하고 있따
- 절차형 SQL을 이용하여 SQL문의 연속적인 실행이나 조건에 따른 분기처리를 이용하여 특정 기능을 수행하는 저장 모듈을 생성할 수 있따
- 절차형 SQL을 이용하여 PROCEDURE, TRIGGER, USER DEFINED FUNCTION을 만들 수 있따
- PL/SQL과 관련된 내용은 상당히 다양하고 분량이 많기 때문에 상세한 내역은 각 DBMS 벤더의 매뉴얼을 참조한다

**PL/SQL 특징**

- Oracle의 PL/SQL은 Block 구조로 되어있고 Block 내에는 DML 문장과 QUERY 문장, 그리고 절차형 언어(IF, LOOP)등을 사용할 수 있으며, 절차적 프로그래밍을 가능하게 하는 트랜잭션 언어이다
- PL/SQL을 이용하여 다양한 저장 모듈(Stored Module)을 개발할 수 있다
- 저장 모듈이란 PL/SQL 문장을 데이터베이스 서버에 저장하여 사용자와 애플리케이션 사이에서 공유할 수 있도록 만든 일종의 SQL 컴포넌트 프로그램이며, 독립적으로 실행되거나 다른 프로그램으로부터 실행될 수 있는 완전한 실행 프로그램이다
- 데이터베이스 내부에 저장됨으로 인해서 관리적인 문제가 발생할 수 있다
- 일반적으로 3개의 유형 중에는 데이터 무결성 및 데이터 집계를 위해 트리거 사용빈도가 높다
- 프로시저의 경우 DBA 외에 일반 사용자가 사용하는 경우가 적음
- 스칼라 서브쿼리 이후 사용자정의함수의 사용 빈도는 줄어들고 있음

***

- PL/SQL은 Block 구조로 되어있어 각 기능별로 모듈화가 가능하다
- 변수, 상수 등을 선언하여 SQL 문장 간 값을 교환한다
- IF, LOOP 등의 절차형 언어를 사용하여 절차적인 프로그램이 가능하도록 한다
- DBMS 정의 에러나 사용자 정의 에러를 정의하여 사용할 수 있다
- PL/SQL은 Oracle에 내장되어 있으므로 Oracle과 PL/SQL을 지원하는 어떤 서버로도 프로그램을 옮길 수 있따
- PL/SQL은 응용 프로그램의 성능을 향상시킨다
- PL/SQL은 여러 SQL 문장을 Block으로 묶고 한 번에 Block 전부를 서버로 보내기 때문에 통신량을 줄일 수 있다

**PL/SQL 엔진**

- PL/SQL 엔진은 PL/SQL Block 프로그램을 입력받으면 SQL 문장과 프로그램 문장을 구분하여 처리한다
- 즉 프로그램 문장은 PL/SQL 엔진이 처리하고 SQL 문장은 Oracle 서버의 SQL Statement Executor가 실행하도록 작업을 분리하여 처리한다
- ![스크린샷 2023-11-15 오후 10.31.17](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 10.31.17.png)

**PL/SQL 블록 구조**

- ![스크린샷 2023-11-15 오후 10.31.50](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 10.31.50.png)

**PL/SQL 기본 문법(Syntax)**

- ![스크린샷 2023-11-15 오후 10.32.25](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 10.32.25.png)
- CREATE TABLE 명령어로 테이블을 생성하듯 CREATE 명령어로 데이터베이스 내에 프로시저를 생성할 수 있다. 삭제는 DROP 명령어 사용함
- [OR REPLACE] 절은 데이터베이스 내에 같은 이름의 프로시저가 있을 경우, 기존의 프로시저를 무시하고 새로운 내용으로 덮어쓰기 하겠다는 의미이다
- argument는 프로시저가 호출될 때 프로시저 안으로 어떤 값이 들어오거나 혹은 프로시저에서 처리한 결과값을 운영 체제로 리턴시킬 매개 변수를 지정할 때 사용한다
- [mode] 부분에 지정할 수 있는 매개 변수의 유형은 3가지가 있다
  - IN은 운영 체제에서 프로시저로 전달될 변수의 MODE이고,
  - OUT은 프로시저에서 처리된 결과가 운영체제로 전달되는 MODE이다
  - 마지막으로 잘 쓰지는 않지만 INOUT MODE가 있는데 이 MODE는 IN과 OUT 두 가지의 기능을 동시에 수행하는 MODE 이다.
- 마지막에 있는 슬래쉬("/")는 데이터베이스에게 프로시저를 컴파일하라는 명령어이다

**Procedure 생성**

- ![스크린샷 2023-11-15 오후 10.42.54](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 10.42.54.png)
- ![스크린샷 2023-11-15 오후 10.43.07](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 10.43.07.png)
  1. DEPT 테이블에 들어갈 칼럼 값(부서코드, 부서명, 위치)을 입력 받는다
  2. 입력받은 부서코드가 존재하는지 확인한다
  3. 부서코드가 존재하면 '이미 등록된 부서번호입니다'라는 메시지를 출력값에 넣는다
  4. 부서코드가 존재하지 않으면 입력받은 필드 값으로 새로운 부서 레코드를 입력한다
  5. 새로운 부서가 정상적으로 입력됐을 경우에는 COMMIT 명령어를 통해서 트랜잭션을 종료한다
  6. 에러가 발생하면 모든 트랜잭션을 취소하고 'ERROR 발생' 이라는 메시지를 출력값에 넣는다

**Procedure 활용**

- ![스크린샷 2023-11-16 오전 12.45.42](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.45.42.png)
- ![스크린샷 2023-11-16 오전 12.45.51](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.45.51.png)
  1. DEPT 테이블을 조회하면 총 4개 행의 결과가 출력된다
  2. Procedure을 실행한 결과값을 받을 변수를 선언한다(BIND 변수)
  3. 존재하는 DEPTNO(10)을 가지고 Procedure을 실행한다
  4. DEPTNO가 10인 부서는 이미 존재하기 때문에 변수 rslt를 print 해보면 '이미 등록된 부서번호이다' 라고 출력된다
  5. 이번에는 새로운 DEPTNO(50)를 가지고 입력한다
  6. rslt를 출력해 보면 '입력 완료!' 라고 출력된다
  7. DEPT 테이블을 조회하여 보면 DEPTNO가 50인 데이터가 정확하게 저장되었음을 확인할 수 있다

**사용자 정의 함수 (User Definded Function)**

- User Defined Function은 Procedure처럼 절차형 SQL을 로직과 함께 데이터베이스 내에 저장해 놓은 명령문의 집합을 의마한다. 앞에서 학습한 SUM, SUBSTR, NVL 등의 함수는 벤더에서 미리 만들어둔 내장 함수이고, 사용자가 별도의 함수를 만들 수도 있다
- Function이 Procedure와 다른 점은 RETURN을 사용해서 일반적으로 하나의 값을 반드시 되돌려 줘야 한다는 것이다. 즉 Function은 Procedure와는 달리 SQL 문장에서 특정 작업을 수행하고 반드시 수행 결과값을 리턴한다.

**User Definded Function 생성**

- ![스크린샷 2023-11-16 오전 12.49.42](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.49.42.png)

**User Definded Function 활용**

- ![스크린샷 2023-11-16 오전 12.50.01](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.50.01.png)

**Trigger**

- Trigger란 특정한 테이블에 INSERT, UPDATE, DELETE 같은 DML문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 작성된 프로그램이다
- 사용자가 직접 호출하여 사용하는 것이 아니고, 생성 이후 조건이 맞으면 데이터베이스에서 자동적으로 수행하게 된다
- Trigger는 테이블과 뷰, 데이터베이스 작업을 대상으로 정의할 수 있으며, 전체 트랜잭션 작업에 대해 발생되는 Trigger와 각 행에 대해서 발생되는 Trigger가 있다
- 데이터웨어하우스의 실시간 집계성 테이블이나, Materialized View 생성시 사용할 수 있다
- 데이터 무결성을 위해 FK 역할을 수행할 수도 있다
- Trigger는 데이터베이스 보안의 적용, 유효하지 않은 트랜잭션의 예방, 업무 규칙의 적용, 감사 제공 등에 사용될 수 있다
- OLTP성의 계정계, 기간계 시스템에서는 성능 부하를 발생할 위험이 있다.

**Trigger 생성**

- ![스크린샷 2023-11-16 오전 12.56.54](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.56.54.png)
- ![스크린샷 2023-11-16 오전 12.57.03](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.57.03.png)
- ![스크린샷 2023-11-16 오전 12.57.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.57.14.png)

**Trigger 활용**

- ![스크린샷 2023-11-16 오전 12.57.27](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.57.27.png)
- ![스크린샷 2023-11-16 오전 12.57.35](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.57.35.png)

**프로시저(Procedure)와 트리거의 차이점**

- 프로시저는 BEGIN ~ END 절 내에 COMMIT, ROLLBACK과 같은 트랜잭션 종료 명령어를 사용할 수 있지만, 데이터베이스 트리거는 BEGIN ~ END 절 내에 사용할 수 없다
- ROLLBACK을 하면 원 트랜잭션 뿐만 아니라 Trigger로 입력된 정보까지 하나의 트랜잭션으로 인식하여 두 테이블 모두 입력 취소가 된다. Trigger는 데이터베이스에 의해 자동 호출되지만 결국 INSERT, UPDATE, DELETE 문과 하나의 트랜잭션 안에서 일어나는 일련의 작업들이라 할 수 있다
- ![스크린샷 2023-11-16 오전 12.59.21](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-16 오전 12.59.21.png)

