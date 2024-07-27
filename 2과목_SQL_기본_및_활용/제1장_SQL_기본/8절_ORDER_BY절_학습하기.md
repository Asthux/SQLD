**ORDER BY 정렬**

- ORDER BY 절은 SQL 문장으로 조회된 데이터들을 다양한 목적에 맞게 특정 칼럼을 기준으로 정렬하여 출력하는데 사용한다

- ORDER BY 절에 칼럼(Column)명 대신에 SELECT 절에서 사용한 ALIAS 명이나 칼럼 순서를 나타내는 정수도 사용 가능하다. SELECT 절의 칼럼명이 길거나 정렬 조건이 많을 경우 편리하게 사용할 수 있으나, 향후 유지보수성이나 가독성이 떨어지므로 가능한 칼럼명이나 ALIAS 명을 권고한다. ORDER BY 절에서 칼럼명, ALIAS명, 칼럼 순서를 같이 혼용하는 것도 가능하다

- 별도로 정렬 방식을 지정하지 않으면 기본적으로 오름차순이 적용되며, SQL 문장의 제일 마지막에 위치한다

- Oracle은 NULL 값을 가장 큰 값으로 취급한다. 반면 SQL Server는 최소값으로 간주한다

- ![스크린샷 2023-11-03 오후 3.47.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 3.47.33.png)

- ![스크린샷 2023-11-03 오후 3.58.19](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 3.58.19.png)

- GROUP BY 절과 ORDER BY가 같이 사용될 때 SELECT SQL 문장은 6개의 절로 구성이 되고, SELECT SQL 문장의 수행 단계는 아래와 같다. 아래는 옵티마이저가 SQL 문장의 SYNTAX 에러를 점검하는 순서이기도 하다.

  5. SELECT 칼럼명(ALIAS명)

  1. FROM 테이블명

  2. WHERE 조건식

  3. GROUP BY 칼럼(Column)이나 표현식

  4. HAVING 그룹조건식

  6. ORDER BY 칼럼(Column)이나 표현식;

- 1. 발췌 대상 테이블을 참조한다.(FROM)
  2. 발췌 대생 데이터가 아닌 것은 제거한다.(WHERE)
  3. 행들을 소그룹화 한다.(GROUP BY)
  4. 그룹핑된 값의 조건에 맞는 것만을 출력한다.(HAVING)
  5. 데이터 값을 출력/계산한다.(SELECT)
  6. 데이터를 정렬한다.(ORDER BY)

- FROM 절에 정의되지 않은 테이블의 칼럼을 WHERE 절, GROUP BY 절, HAVING 절, SELECT 절, ORDER BY 절에서 사용하면 에러가 발생한다

- 그러나, ORDER BY 절에는 SELECT 목록에 나타나지 않은 문자형 항목이 포함될 수 있다. (단, SELECT DISTINCT를 지정하거나 문에 GROUP BY 절이 있거나 또는 SELECT 문에 UNION 연산자가 있으면 열 이름이 SELECT 목록에 나타나야 한다)![스크린샷 2023-11-03 오후 4.40.24](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.40.24.png)

- 관계형 데이터베이스가 데이터를 메모리에 올릴 때 행 단위로 모든 칼럼을 가져오게 되므로, SELECT 절에서 일부 칼럼만 선택하더라도 ORDER BY 절에서 메모리에 올라와 있는 다른 칼럼의 데이터를 사용할 수 있다. (단위 SQL 기준이며 서브쿼리를 벗어나는 경우 SELECT 절에 정의된 칼럼만 메인쿼리에서 재사용될 수 있다)

- 실행 결과에서 2장에서 배울 인라인 뷰의 SELECT 절에서 정의한 칼럼만 메인쿼리에서 사용할 수 있는 것을 확인할 수 있다 (서브쿼리 동일)

- ![스크린샷 2023-11-03 오후 4.41.47](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.41.47.png)

- GROUP BY 절에서 그룹핑 기준을 정의하게 되면 DBMS는 일반적인 SELECT 문장처럼 FROM 절에 정의된 테이블의 구조를 그대로 가지고 가는 것이 아니라, GROUP BY 절의 그룹핑 기준으로 행들을 소그룹화 한다

- ![스크린샷 2023-11-03 오후 4.42.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.42.33.png)

- GROUP BY 절이 사용되었을 경우 GROUP BY 절의 그룹핑 기준으로 소그룹화된 데이터를 활용해서, SELECT 절에 정의하지 않은 MAX, SUM, COUNT 같은 집계함수를 ORDER BY 절에서 사용할 수 있는 것을 확인할 수 있다

- ![스크린샷 2023-11-03 오후 4.43.21](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.43.21.png)

**TOP N 쿼리**

- 5절 WHERE절에서 사용한 ROWNUM 사용시 주의할 점을 소개한다
- Oracle의 경우 ORDER BY 절과 WHERE 절의 ROWNUM 조건을 같이 사용하는 경우 정렬이 완료된 데이터의 일부가 출력되는 것이 아니라, 데이터의 일부가 먼저 추출된 후 데이터에 대한 정렬 작업이 일어나므로 원하는 데이터를 얻지 못할 수 있다
- ![스크린샷 2023-11-03 오후 4.44.28](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.44.28.png)
- 실행 결과의 3명은 급여가 상위인 3명을 출력한 것이 아니라, 무작위로 추출된 3명에 한해서(WHERE절 우선 수행) 급여를 내림차순으로 정렬한 결과이므로 문법적 오류가 발생하지 않더라도 업무적으로 잘못된 결과를 출력한 것이다
- ![스크린샷 2023-11-03 오후 4.45.09](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.45.09.png)
- EMP 테이블의 데이터를 급여가 많은 순서부터 인라인 뷰에서 정렬을 먼저 수행한 후 상위 3건의 데이터를 출력한 것이다
- ORDER BY 절이 없으면 Oracle의 Rownum 조건과 SQL Server의 TOP 절은 같은 결과를 보인다. 그렇지만, ORDER BY 절이 사용되는 경우 Oracle은 Rownum 조건을 ORDER BY 절보다 먼저 처리되는 WHERE 절에서 처리하므로 정렬 후 원하는 데이터를 얻기 위해서는 위처럼 먼저 인라인뷰로 가공하는 절차를 거쳐야 한다.
- 반면 SQL Server는 TOP 조건을 사용하게 되면 별도 처리 없이 관련 ORDER BY 절의 데이터 정렬 후 원하는 일부 데이터만 쉽게 출력할 수 있다
- ![스크린샷 2023-11-03 오후 4.46.49](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-03 오후 4.46.49.png)