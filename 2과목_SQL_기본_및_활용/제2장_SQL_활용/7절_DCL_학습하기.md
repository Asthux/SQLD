**DCL**

- 유저를 생성하고 권한을 제어할 수 있는 DCL(DATA CONTROL LANGUAGE) 명령어가 있다
- 대부분의 데이터베이스는 데이터 보호와 보안을 위해서 유저와 권한을 관리하고 있다
- 예를 들어 Oracle을 설치하면 기본적으로 제공되는 유저들인 SYS, SYSTEM, SCOTT 유저에 대해서 간단하게 알아본다
- ![스크린샷 2023-11-15 오후 5.17.07](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.17.07.png)

**시스템 권한**

- Oracle의 DBA 권한을 가지고 있는 SYSTEM 유저로 접속하면 유저 생성 권한(CREATE USER)을 다른 유저에게 부여할 수 있다
- ![스크린샷 2023-11-15 오후 5.17.56](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.17.56.png)

**SESSION 생성 권한**

- Oracle의 PJS 유저가 생성됐지만 아무런 권한도 부여받지 못했기 때문에 로그인을 하면 CREATE SESSION 권한이 없다는 오류가 발생한다
- ![스크린샷 2023-11-15 오후 5.18.44](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.18.44.png)

**TABLE 생성 권한**

- Oracle의 PJS 유저는 로그인 권한만 부여되었기 때문에 테이블을 생성하려면 테이블 생성 권한(CREATE TABLE)이 불충분하다는 오류가 발생한다
- ![스크린샷 2023-11-15 오후 5.19.25](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.19.25.png)

**오브젝트 권한**

- Oracle의 오브젝트(객체) 권한은 특정 오브젝트인 테이블, 뷰 등에 대한 SELECT, INSERT, DELETE, UPDATE 작업 명령어를 의미한다
- ![스크린샷 2023-11-15 오후 5.20.10](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.20.10.png)
- ![스크린샷 2023-11-15 오후 5.20.24](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.20.24.png)

**ROLE을 이용한 권한 부여**

- Oracle의 데이터베이스 관리자는 유저가 생성될 때마다 각각의 권한들을 유저에게 부여하는 작업을 수행해야 하는데, 효율적인 관리를 위해 유저들과 권한들 사이에서 중개 역할을 하는 ROLE을 제공한다
- 왼쪽 그림은 권한을 직접 유저에게 할당할 때를 나타내는 것이며, 오른쪽 그림은 ROLE에 권한을 부여한 후 ROLE을 유저들에게 부여하는 것을 나타내고 있다
- ![스크린샷 2023-11-15 오후 5.21.40](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.21.40.png)

**ROLE을 이용한 권한 부여**

- ![스크린샷 2023-11-15 오후 5.21.58](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.21.58.png)
- Oracle에서 가장 많이 사용하는 ROLE은 CONNECT와 RESOURCE이다
- CONNECT는 CREATE SESSION과 같은 로그인 권한이 포함되어 있고, RESOURCE는 CREATE TABLE과 같은 오브젝트 생성 권한이 포함되어 있다
- 일반적을 Oracle에서 유저를 생성할 때 CONNECT와 RESOURCE ROLE을 사용하여 기본 권한을 부여한다
- ![스크린샷 2023-11-15 오후 5.23.05](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 5.23.05.png)

**SQL Server 로그인**

1. Windows 인증 방식으로 Windows에 로그인한 정보를 가지고 SQL Server에 접속하는 방식이다. Microsoft Windows 사용자 계정을 통해 연결되면 SQL Server는 운영 체제의 Windows 보안 주체 토큰을 사용하여 계정 이름과 암호가 유효한지 확인한다. 즉, Windows에서 사용자 ID를 확인한다. SQL Server는 암호를 요청하지 않으며 ID의 유효성 검사를 수행하지 않는다
2. 혼합 모드(Windows 인증 또는 SQL 인증) 방식으로 기본적으로 Windows 인증으로도 SQL Server에 접속 가능하며, Oracle의 인증과 같은 방식으로 사용자 아이디와 비밀번호로 SQL Server에 접속하는 방식이다. SQL 인증을 사용할 때는 암호(숫자+문자+특수문자 등을 혼합하여 사용)를 사용해야 한다

**SQL Server 권한**

- SQL Server에서는 Oracle과 같이 Role을 자주 사용하지 않는다. 대신 위에서 언급한 서버 수준 역할 및 데이터베이스 수준 역할을 이용하여 로그인 및 사용자 권한을 제어한다
- 인스턴스 수준의 작업이 필요한 경우 서버 수준 역할을 부여하고 그보다 작은 개념인 데이터베이스 수준의 권한이 필요한 경우 데이터베이스 수준의 역할을 부여하면 된다
- 즉, 인스턴스 수준을 요구하는 로그인에는 서버 수준 역할을, 데이터베이스 수준을 요구하는 사용자에게는 데이터베이스 수준 역할을 부여한다.
- 