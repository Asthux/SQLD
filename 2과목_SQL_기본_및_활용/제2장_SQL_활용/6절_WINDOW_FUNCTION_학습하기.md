**데이터 분석 함수(ANSI/ISO-SQL표준)**

- AGGREGATE FUNCTIONS
  - GROUP FUNCTION의 한 부분이며, GROUP AGGREGATE FUNCTION 이라고도 부를 수 있다. 1장 7절에서 배웠던 COUNT, SUM, AVG, MAX, MIN 외 각종 집계 함수들이 포함되어 있다
- GROUP FUNCTIONS
  - 그룹 함수로는 집계 함수를 제외하면, 소그룹 간의 소계를 계산하는 ROLLUP 함수, GROUP BY 항목들간의 다차원적인 소계를 계산할 수 있는 CUBE 함수, 특정 항목에 대한 소계를 계산하는 GROUPING SETS 함수가 있다
- WINDOW FUNCTIONS
  - 분석 함수(ANALYTIC FUNCTION)나 순위 함수(RANK FUNCTION)로도 알려져 있는 윈도우 함수(ANSI/ISO-SQL은 WINDOW FUNCTION 용어 사용)는 데이터웨어하우스에서 발전한 기능이며, 부분적이나마 행과 행 간의 관계를 쉽게 정의하기 위해 만든 함수이다

**WINDOW FUNCTION**

- 기존 관계형 데이터베이스는 칼럼과 칼럼간의 연산, 비교, 연결이나 집합에 대한 집계는 쉬운 반면, 행과 행간의 관계를 정의하거나, 행과 행간을 비교, 연산하는 것을 하나의 SQL 문으로 처리 하는 것은 매우 어려운 문제였다
- 부분적이나마 행과 행 간의 관계를 쉽게 정의하기 위해 만든 함수가 바로 WINDOW FUNCTION이다. 윈도우 함수를 활용하면 복잡한 프로그램을 하나의 SQL 문장으로 쉽게 해결할 수 있다
- 복잡하거나 자원을 많이 사용하는 튜닝 기법들을 대체할 수 있는 DBMS의 새로운 기능은 튜닝 관점에서도 최적화된 방법이므로 적극적으로 활용할 필요가 있다. 같은 결과가 나오는 수정된 튜닝 문장보다는 DBMS 벤더에서 최적화된 자원을 사용하도록 만들어진 새로운 기능을 사용하는 것이 일반적으로 더욱 효과가 좋기 때문이다
- WINDOW 함수는 기존에 사용하던 집계 함수도 있고, 새로이 WINDOW 함수 전용으로 만들어진 기능도 있다. 그리고, WINDOW 함수는 다른 함수와는 달리 중첩(NEST)해서 사용하지는 못하지만, 서브 쿼리에서는 사용할 수 있다

**WINDOW FUNCTION 종류**

1. 그룹 내 순위(RANK)관련 함수는 RANK, DENSE_RANL, ROW_NUMBER 함수가 있다. ANSI/ISO-SQL 기준과 ORACLE, SQL-SERVER 등 대부분의 DBMS에서 지원하고 있다
2. 그룹 내 집계(AGGREGATE) 관련 함수는 일반적으로 많이 사용하는 SUM, MAX, MIN, AVG, COUNT 함수가 있다.  ANSI/ISO-SQL 기준과 ORACLE, SQL-SERVER 등 대부분의 DBMS에서 지원하고 있는데, SQL SERVER의 집계 함수는 뒤에서 설명할 OVER 절 내의 ORDER BY 구문을 지원하지 않는다
3. 그룹 내 행 순서 관련 함수는 FIRST_VALUE, LAST_VALUE, LAG, LEAD 함수가 있다. ORACLE에서만 지원되는 함수이다
4. 그룹 내 비율 관련 CUME_DIST, PERCENT_RANK 함수는 ANSI/ISO-SQL 기준과 ORACLE, SQL-SERVER 등 대부분의 DBMS에서 지원하고 있다. NTILE 함수는 ANSI/ISO-SQL 기준에는 없지만, ORACLE, SQL-SERVER에서 지원하고 있다. 마지막으로 RATIO_TO_REPORT 함수는 ORACLE에서만 지원되는 함수이다.
5. 선형 분석을 포함한 통계 분석 관련 함수가 있는데, 통계에 특화된 기능이므로 본 과정에서는 설명을 생략한다

**WINDOW FUNCTION SYNTAX**

- ![스크린샷 2023-11-15 오후 4.03.05](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.03.05.png)
- WINDOW FUNCTION : 기존에 사용하던 함수도 있고, 새롭게 WINDOW 함수용으로 추가된 함수도 있다
- ARGUMENTS (인수) : 함수에 따라 0~N 개의 인수가 지정될 수 있다
- OVER : WINDOW 함수에는 OVER 문구가 키워드로 꼭 포함된다
- PARTITION BY 절 : 전체 집합을 기준에 의해 소그룹으로 나눌 수 있다
- ORDER BY 절 : 어떤 항목에 대해 순위를 지정할 지 ORDER BY 절을 기술한다
- WINDOWING 절 : WINDOWING 절은 함수의 대상이 되는 행 기준의 범위를 강력하게 지정할 수 있다
  - ROWS는 물리적이니 결과 행의 수를, RANGE는 논리적인 값에 의한 범위를 나타내는데, 둘 중 하나를 선택해서 사용할 수 있다

**RANK 함수**

- RANK 함수는 ORDER BY를 포함한 QUERY 문에서 특정 항목(칼럼)에 대한 순위를 구하는 함수이다. 이때 특정 범위(PARTITION) 내에서 순위를 구할 수도 있고 전체 데이터에 대한 순위를 구할 수도 있다. 또한 동일한 값에 대해서는 동일한 순위를 부여하게 된다
- ![스크린샷 2023-11-15 오후 4.07.39](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.07.39.png)
- ![스크린샷 2023-11-15 오후 4.08.01](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.08.01.png)

**DENSE_RANK 함수**

- DENSE_RANK 함수는 RANK 함수와 흡사하나, 동일한 순위를 하나의 건수로 취급하는 것이 틀린 점이다.
- ![스크린샷 2023-11-15 오후 4.08.38](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.08.38.png)
- ![스크린샷 2023-11-15 오후 4.08.51](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.08.51.png)

**ROW_NUMBER 함수**

- ROW_NUMBER 함수는 RANK나 DENSE_RANK 함수가 동일한 값에 대해서는 동일한 순위를 부여하는데 반해, 동일한 값이라도 유니크한 순위를 부여한다.
- ![스크린샷 2023-11-15 오후 4.09.32](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.09.32.png)
- ![스크린샷 2023-11-15 오후 4.09.44](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.09.44.png)

**MAX 함수**

- MAX 함수를 이용해 파티션별 윈도우의 최대값을 구할 수 있다
- ![스크린샷 2023-11-15 오후 4.10.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.10.11.png)
- ![스크린샷 2023-11-15 오후 4.10.22](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.10.22.png)
- ![스크린샷 2023-11-15 오후 4.10.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.10.33.png)

**MIN 함수**

- MIN 함수를 이용해 파티션별 윈도우의 최소값을 구할 수 있다
- ![스크린샷 2023-11-15 오후 4.10.58](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.10.58.png)
- ![스크린샷 2023-11-15 오후 4.11.08](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.11.08.png)

**SUM 함수**

- SUM 함수를 이용해 파티션별 윈도우의 합을 구할 수 있다
- ![스크린샷 2023-11-15 오후 4.11.32](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.11.32.png)
- ![스크린샷 2023-11-15 오후 4.11.40](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.11.40.png)

**AVG 함수**

- AVG 함수와 파티션별 ROWS 윈도우를 이용해 원하는 조건에 맞는 데이터에 대한 통계값을 구할 수 있다
- ![스크린샷 2023-11-15 오후 4.12.15](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.12.15.png)
- ![스크린샷 2023-11-15 오후 4.12.24](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.12.24.png)

**COUNT 함수**

- COUNT 함수와 파티션별 ROWS 윈도우를 이용해 원하는 조건에 맞는 데이터에 대한 통계값을 구할 수 있다
- ![스크린샷 2023-11-15 오후 4.12.55](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.12.55.png)
- ![스크린샷 2023-11-15 오후 4.13.06](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.13.06.png)

**FIRST_VALUE 함수**

- FIRST_VALUE 함수를 이용해 파티션별 윈도우에서 가장 먼저 나온 값을 구한다
- ![스크린샷 2023-11-15 오후 4.13.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.13.33.png)
- ![스크린샷 2023-11-15 오후 4.13.42](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.13.42.png)

**LAST VALUE 함수**

- LAST_VALUE 함수를 이용해 파티션별 윈도우에서 가장 나중에 나온 값을 구한다
- ![스크린샷 2023-11-15 오후 4.14.08](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.14.08.png)
- ![스크린샷 2023-11-15 오후 4.14.18](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.14.18.png)

**LAG 함수**

- LAG 함수를 이용해 파티션별 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다

- #### ![스크린샷 2023-11-15 오후 4.14.45](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.14.45.png)

- ![스크린샷 2023-11-15 오후 4.14.57](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.14.57.png)

**LEAD 함수**

- LEAD 함수를 이용해 파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다.
- ![스크린샷 2023-11-15 오후 4.30.39](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.30.39.png)

**RATION_TO_REPORT 함수**

- RATIO_TO_REPORT 함수를 이용해 파티션 내 전체 SUM(칼럼)값에 대한 행별 칼럼값의 백분율을 소수점으로 구할 수 있다. 결과값은 > 0 & <= 1 의 범위를 가진다. 그리고, 개별 RATIO의 값을 구하면 1이 된다
- ![스크린샷 2023-11-15 오후 4.32.24](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.32.24.png)

**PERCENT_RANK 함수**

- PERCENT_RANK 함수를 이용해 파티션별 윈도우에서 제일 먼저 나오는 것을 0으로, 제일 늦게 나오는 것을 1으로 하여, 값이 아닌 행의 순서별 백분율을 구한다. 결과값은 >= 0 & <= 1 의 범위를 가진다.
- ![스크린샷 2023-11-15 오후 4.33.25](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.33.25.png)
- ![스크린샷 2023-11-15 오후 4.33.36](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.33.36.png)

**CUME_DIST 함수**

- CUME_DIST 함수를 이용해 파티션별 윈도우의 전체건수에서 현재 행보다 작거나 같은 건수에 대한 누적백분율을 구한다. 결과값은 > 0 & <= 1 의 범위를 가진다.
- ![스크린샷 2023-11-15 오후 4.34.28](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.34.28.png)
- ![스크린샷 2023-11-15 오후 4.34.36](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.34.36.png)

**NTILE 함수**

- NTILE 함수를 이용해 파티션별 전체 건수를 ARGUMENT 값으로 N 등분한 결과를 구할 수 있다

- ![스크린샷 2023-11-15 오후 4.35.06](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.35.06.png)

- ![스크린샷 2023-11-15 오후 4.35.17](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-15 오후 4.35.17.png)

  