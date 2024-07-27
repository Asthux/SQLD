**WHERE 절**

- 원하는 자료만을 검색하기 위해서 SQL 문장에 WHERE 절을 이용하여 자료들에 대하여 제한할 수 있다
- 두 개 이상의 테이블에 대한 INNER JOIN을 지원하는 다른 기능도 가지고 있따
- 조회하려는 데이터에 특정 조건을 부여할 목적으로 사용하기 때문에 FROM 절 뒤에 오게 된다
- ![스크린샷 2023-10-31 오후 8.53.59](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 8.53.59.png)

**연산자 종류**

![스크린샷 2023-10-31 오후 8.54.19](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 8.54.19.png)

![스크린샷 2023-10-31 오후 8.55.15](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 8.55.15.png)

**연산자 우선 순위**

![스크린샷 2023-10-31 오후 8.55.38](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 8.55.38.png)

- 실수하기 쉬운 비교 연산자와 논리 연산자의 경우 괄호를 사용해서 우선 순위를 표시하는 것을 권고한다

**WHERE 조건**

- CHAR 변수나 VARCHAR2와 같은 문자형 타입을 가진 칼럼을 특정 값과 비교하기 위해서는 인용 부호(작은 따옴표, 큰 따옴표)로 묶어서 비교 처리를 해야 한다
- NUMERIC과 같은 숫자형 형태의 값은 인용부호를 사용하지 않는다![스크린샷 2023-10-31 오후 9.03.10](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.03.10.png)
- ![스크린샷 2023-10-31 오후 9.03.34](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.03.34.png)
- ![스크린샷 2023-10-31 오후 9.03.50](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.03.50.png)

**WHERE 조건 - IS NULL**

- NULL : 아직 정의되지 않은 미지의 값, 또는 현재 알 수 없는 값
- NULL 값과의 수치연산은 NULL 값을 리턴한다
- NULL 값과의 비교연산은 거짓(FALSE)를 리턴한다, 오라클의 경우 문법적으로 '= NULL' 조건에서 오류가 발생하지는 않지만, 데이터는 1건도 검색되지 않는다
- 어떤 값과 비교할 수 없으며 특정 값보다 크다, 작다라고 표현할 수 없다
- NULL 값의 비교 연산은 IS NULL, IS NOT NULL 이라는 정해진 문구를 사용해야 제대로 된 결과를 얻을 수 있다
- ![스크린샷 2023-10-31 오후 9.07.04](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.07.04.png)

**WHERE 조건 - 부정연산자**

- ![스크린샷 2023-10-31 오후 9.08.16](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.08.16.png)

**WHERE 조건 - ROWNUM**

- Oracle의 ROWNUM은 Pseudo Column(유사 칼럼, 사용자가 아닌 시스템이 관리하는)으로, 테이블이나 집합에서 원하는 만큼의 행만 가져오고 싶을 때 WHERE 절에서 사용할 수 있다
- ![스크린샷 2023-10-31 오후 9.07.04](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.07.04.png)

**WHERE 조건 - TOP**

- SQL Server는 TOP 절을 사용하여 결과 집합으로 출력되는 행 수를 제한할 수 있다.

- ![스크린샷 2023-10-31 오후 9.10.09](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-31 오후 9.10.09.png)

  

