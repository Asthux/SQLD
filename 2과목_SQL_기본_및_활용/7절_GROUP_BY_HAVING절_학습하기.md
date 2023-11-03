**집계 함수(Aggregate Function)**

다중행 함수 중 집계 함수(Aggregate Function)의 특성은 다음과 같다

- 여러 행들의 그룹이 모여서 그룹당 단 하나의 결과를 돌려주는 함수
- SELECT, HAVING, ORDER BY 절에 사용할 수 있다
- 테이블 전체 집계를 위해 GROUP BY 절 없이도 집계 함수를 사용할 수 있다
- 집계 함수는 그룹에 대한 정보를 제공하므로 주로 숫자 유형에 사용되지만, MAX, MIN, COUNT 함수는 문자, 날짜 유형에도 적용이 가능한 함수이다
- ![스크린샷 2023-11-02 오후 3.35.05](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 3.35.05.png)
- ![스크린샷 2023-11-02 오후 3.35.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 3.35.33.png)
- ![스크린샷 2023-11-02 오후 3.35.47](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 3.35.47.png)

**GROUP BY 절**

- GROUP BY 절은 SQL 문에서 FROM 절과 WHERE 절 뒤에 오며 GROUP BY 절은 행들을 소그룹화 한다
- 데이터들을 작은 그룹으로 분류하여 소그룹에 대한 항목별로 통계 정보를 얻을 때 추가로 사용된다
- GROUP BY 절과 HAVING 절은 다음과 같은 특성을 가진다
  - GROUP BY 절을 통해 소그룹별 기준을 정한 후, SELECT 절에 집계 함수를 사용한다
  - GROUP BY 절에서는 SELECT 절과는 달리 칼럼 ALIAS 명을 사용할 수 없다
  - WHERE 절은 전체 데이터를 GROUP으로 나누기 전에 행들을 미리 제거시킨다
  - GROUP BY 절과 HAVING 절의 순서를 바꾸더라도 문법 에러가 없고 결과물도 동일한 결과를 출력한다. 그렇지만, 논리적으로 GROUP BY 절과 HAVING 절의 순서를 지키는 것을 권고한다
  - 집계 함수의 통계 정보는 NULL 값을 가진 행을 제외하고 수행한다
  - HAVING 절은 GROUP BY 절의 기준 항목이나 소그룹의 집계 함수를 이용한 조건을 표시할 수 있다
  - 집계 함수는 WHERE 절에는 올 수 없다
  - GROUP BY 절에 의한 소그룹별로 만들어진 집계 데이터 중, HAVING 절에서 제한 조건을 두어 조건을 만족하는 내용만 출력한다
  - 일부 데이터베이스의 과거 버전에서는 데이터베이스가 GROUP BY 절에 명시된 칼럼(Column)의 순서대로 오름차순 정렬을 자동으로 실시하는 경우가 있었으나, 지금은 정렬을 위해서는 뒤에서 언급할 ORDER BY 절을 명시해야 정렬이 수행된다
- ![스크린샷 2023-11-02 오후 3.40.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 3.40.11.png)
- ![스크린샷 2023-11-02 오후 3.40.23](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 3.40.23.png)

**HAVING 절**

- HAVING 절은 WHERE 절과 비슷하지만 GROUP BY 절에 의해 만들어진 소그룹에 대한 조건이 적용된다는 점에서 차이가 있다
- ![스크린샷 2023-11-02 오후 4.24.15](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.24.15.png)

- HAVING 절은 SELECT 절에 사용되지 않은 칼럼이나 집계 함수가 아니더라도 GROUP BY 절의 기준 항목이나 소그룹의 집계 함수를 이용한 조건을 표시할 수 있다
- ![스크린샷 2023-11-02 오후 4.24.56](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.24.56.png)

**CASE 표현을 활용한 월별 데이터 집계**

- 집계 함수(CASE()~GROUP BY) 기능은, 모델링의 제1정규화로 인해 반복되는 칼럼의 경우 구분 칼럼을 두고 여러 개의 레코드로 만들어진 집합을, 정해진 칼럼 수만큼 확장해서 집계 보고서를 만드는 유용한 기법이다
- ![스크린샷 2023-11-02 오후 4.26.03](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.26.03.png)
- ![스크린샷 2023-11-02 오후 4.26.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.26.14.png)
- ![스크린샷 2023-11-02 오후 4.26.23](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.26.23.png)

**집계 함수와 NULL 처리**

- 다중 행 함수는 입력 값으로 전체 건수가 NULL 값인 경우만 함수의 결과가 NULL이 나오고 전체 건수 중에서 일부만 NULL인 경우는 NULL인 행을 다중 행 함수의 대상에서 제외한다. 예를 들면 100명 중 10명의 성적이 NULL 값일 때 평균을 구하는 다중 행 함수 AVG를 사용하면 NULL 값이 아닌 90명 성적에 대해서 평균 값을 구하게 된다
- 초급 개발자가 많이 실수하는 것이 Oracle의 SUM(NVL(SAL, 0)), SQL Server의 SUM(ISNULL(SAL, 0)) 연산이다. 개별 데이터의 급여(SAL)가 NULL인 경우는 NULL의 특성으로 자동적으로 연산에서 빠지는 데, 불필요하게 NVL/ISNULL 함수를 사용해 0(Zero)으로 변환시켜 데이터 건수 만큼의 연산이 일어나게 하는 것은 시스템의 자원을 낭비하는 일이다. 리포트 출력 때 NULL이 아닌 0을 표시하고 싶은 경우에는 NVL(SUM(SAL, 0))이나, ISNULL(SUM(SAL, 0))처럼 전체 SUM의 결과가 NULL인 경우(대상 건수가 모두 NULL인 경우)애만 한번 NVL/ISNULL 함수를 사용하면 된다
- CASE 표현 사용시 ELSE 절을 생략하게 되면 Default 값이 NULL이다. NULL은 연산의 대상이 아닌 반면, SUM(CASE MONTH WHEN 1 THEN SAL ELSE 0 END)처럼 ELSE 절에서 0(Zero)을 지정하면 불필요하게 0이 SUM 연산에 사용되므로 자원의 사용이 많아진다. 같은 결과를 얻을 수 있다면 가능한 ELSE 절의 상수값을 지정하지 않거나 ELSE 절을 작성하지 않도록 한다. 같은 이유로 Oracle의 DECODE 함수는 4번째 인자를 지정하지 않으면 NULL이 Default로 할당된다.
- ![스크린샷 2023-11-02 오후 4.33.19](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-02 오후 4.33.19.png)

