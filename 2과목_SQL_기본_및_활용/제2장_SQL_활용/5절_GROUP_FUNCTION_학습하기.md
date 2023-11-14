**데이터 분석 함수 (ANSI/ISO-SQL표준)**

- AGGREGATE FUNCTIONS
  - GROUP FUNCTION의 한 부분이며, GROUP AGGREGATE FUNCTION 이라고도 부를 수 있다. 1장 7절에서 배웠던 COUNT, SUM, AVG, MAX, MIN 외 각종 집계 함수들이 포함되어 있다
- GROUP FUNCTIONS
  - 그룹 함수로는 집계함수를 제외하면,
  - 소그룹 간의 소계를 계산하는 ROLLUP 함수,
  - GROUP BY 항목들간의 다차원적인 소계를 계산할 수 있는 CUBE 함수,
  - 특정 항목에 대한 소계를 계산하는 GROUPING SETS 함수가 있다
- WINDOW FUNCTIONS
  - 분석 함수(ANALYTIC FUNCTION)나 순위 함수(RANK FUNCTION)로도 알려져 있는 윈도우 함수는 데이터웨어하우스에서 발전한 기능이며, 자세한 내용은 다음 6절에서 설명한다

**GROUP FUNCTIONS**

- ROLLUP은 GROUP BY의 확장된 형태로 사용하기가 쉬우며 병렬로 수행이 가능하기 때문에 매우 효과적일 뿐 아니라 시간 및 지역처럼 계층적 분류를 포함하고 있는 데이터의 집계에 적합하도록 되어 있다
- CUBE는 결합 가능한 모든 값에 대하여 다차원적인 집계를 생성하게 되므로 ROLLUP에 비해 다양한 데이터를 얻는 장점이 있는 반면에, 시스템에 부하를 많이 주는 단점이 있다
- GROUPING SETS는 원하는 부분의 소계만 손쉽게 추출할 수 있는 장점이 있다
- ROLLUP, CUBE, GROUPING SETS 사용시 정렬이 필요한 경우는 ORDER BY 절에 정렬 칼럼을 명시해야 한다

**ROLLUP 함수**

- ROLLUP에 지정된 Grouping Columns의 List는 Subtotal을 생성하기 위해 사용되어지며, Grouping Columns의 수를 N이라고 했을 때 N+1 Level의 Subtotal이 생성된다
- ROLLUP의 인수는 계층 구조이므로 인수 순서가 바뀌면 수행 결과도 바뀌게 되므로 인수의 순서에도 주의해야 한다
- Oracle을 포함한 일부 DBMS의 과거 버전에서는 GROUP BY 절 사용시 자동적으로 정렬을 수행하였으나, 현재 대부분의 DBMS 버전은 집계 기능만 지원하고 있으며 정렬이 필요한 경우는 ORDER BY 절에 명시적으로 정렬 칼럼이 표시 되어야 한다.

**STEP 1. 일반적인 GROUP BY 절 사용**

- ![스크린샷 2023-11-13 오후 8.56.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-13 오후 8.56.14.png)

**STEP 1-2. GROUP BY 절 + ORDER BY 절 사용**

- ![스크린샷 2023-11-13 오후 8.56.44](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-13 오후 8.56.44.png)

**STEP 2. ROLLUP 함수 사용**

- ![스크린샷 2023-11-14 오후 4.35.45](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.35.45.png)

**STEP 2-2. ROLLUP 함수 + ORDER BY 절 사용**

- ![스크린샷 2023-11-14 오후 4.36.12](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.36.12.png)

**STEP 3. GROUPING 함수 사용**

- ![스크린샷 2023-11-14 오후 4.36.38](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.36.38.png)

**STEP 4. GROUPING 함수 + CASE 사용**

- ![스크린샷 2023-11-14 오후 4.37.07](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.37.07.png)

**STEP 4-2. ROLLUP 함수 일부 사용**

- ![스크린샷 2023-11-14 오후 4.37.28](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.37.28.png)

**STEP 4-3. ROLLUP 함수 결합 칼럼 사용**

- ![스크린샷 2023-11-14 오후 4.37.56](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 4.37.56.png)

**CUBE 함수**

- ROLLUP에서는 단지 가능한 Subtotal만을 생성하였지만, CUBE는 결합 가능한 모든 값에 대하여 다차원 집계를 생성한다. CUBE를 사용할 경우에는 내부적으로는 Grouping Columns의 순서를 바꾸어서 또 한번의 Query를 추가 수행해야 한다. 뿐만 아니라 Grand Total은 양쪽의 Query에서 모두 생성이 되므로 한 번의 Query에서는 제거되어야만 하므로 ROLLUP에 비해 시스템의 연산 대상이 많다
- 이처럼 Grouping Columns이 가질 수 있는 모든 경우에 대하여 Subtotal을 생성해야 하는 경우에는 CUBE를 사용하는 것이 바람직하나, ROLLUP에 비해 시스템에 많은 부담을 주므로 사용에 주의해야 한다
- CUBE 함수의 경우 표시된 인수들에 대한 계층별 집계를 구할 수 있으며, 이때 표시된 인수들 간에는 계층 구조인 ROLLUP 과는 달리 평등한 관계이므로 인수의 순서가 바뀌는 경우 행간에 정렬 순서는 바뀔 수 있어도 데이터 결과는 같다
- CUBE도 결과에 대한 정렬이 필요한 경우는 ORDER BY 절에 명시적으로 정렬 칼럼이 표시가 되어야 한다

**CUBE 함수 이용**

- ![스크린샷 2023-11-14 오후 5.22.38](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.22.38.png)

**STEP 5-2. UNION ALL 사용 SQL**

- ![스크린샷 2023-11-14 오후 5.23.04](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.23.04.png)

**GROUPING SETS 함수**

- GROUPING SETS를 이용해 더욱 다양한 소계 집합을 만들 수 있는데, GROUP BY SQL 문장을 여러 번 반복하지 않아도 원하는 결과를 쉽게 얻을 수 있게 되었다
- GROUPING SETS에 표시된 인수들에 대한 개별 집계를 구할 수 있으며, 이때 표시된 인수들 간에는 계층 구조인 ROLLUP과는 달리 평등한 관계이므로 인수의 순서가 바뀌어도 결과는 같다
- GROUPING SETS 함수도 결과에 대한 정렬이 필요한 경우는 ORDER BY 절에 명시적으로 정렬 칼럼이 표시시가 되어야 한다

**STEP 1. 일반 그룹함수를 이용한 SQL**

- ![스크린샷 2023-11-14 오후 5.25.06](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.25.06.png)

**STEP 2. GROUPING SETS 사용 SQL**

- ![스크린샷 2023-11-14 오후 5.25.30](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.25.30.png)

**STEP 3. 3개의 인수를 이용한 GROUPING SETS 이용**

- ![스크린샷 2023-11-14 오후 5.25.52](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.25.52.png)
- ![스크린샷 2023-11-14 오후 5.26.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-14 오후 5.26.11.png)



