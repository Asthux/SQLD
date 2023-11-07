**STANDARD SQL**

- 현재 우리가 사용하는 많은 시스템의 두뇌 역할을 하는 관계형 데이터베이스를 유일하게 접속할 수 있는 언어가 바로 SQL이다
- SQL에서 ORDBMS 등 필요한 기능을 정리하고 호환 가능한 여러 기준을 제정한 것이 1999년에 정해진 ANSI/ISO-SQL3이다.

**E.F.CODD 일반 집합 연산자**

- 일반 집합 연산자를 현재의 SQL과 비교하면
  1. UNION 연산은 UNION 기능으로(이후 UNION ALL 추가)
  2. INTERSECTION 연산은 INTERSECT 기능으로,
  3. DIFFERENCE 연산은 EXCEPT(Oracle은 MINUS) 기능으로,
  4. PRODUCT 연산은 CROSS JOIN 기능으로 구현되었다

**E.F.CODD 순수 관계 연산자**

- 순수 관계 연산자를 현재의 SQL 문장과 비교하면
  5. SELECT 연산은 WHERE 절로 구현되었다. (SELECT 연산과 SELECT 절 의미 다름)
  6. PROJECT 연산은 SELECT 절로 구현되었다. 
  7. (NATURAL) JOIN 연산은 다양한 JOIN 기능으로 구현되었다
  8. DIVIDE 연산은 현재 사용되지 않는다

**FROM 절 JOIN 형태**

- ANSI/ISO SQL에서 규정한 JOIN 문법은 WHERE 절의 검색 조건과 테이블 간의 JOIN 조건을 구분 없이 사용하던 기존 방식을 그대로 사용할 수 있으면서, 추가된 선택 기능으로 테이블 간의 JOIN 조건을 FROM 절에서 명시적으로 정의할 수 있게 되었다
- INNER JOIN
- NATURAL JOIN
- USING 조건절
- ON 조건절
- CROSS JOIN
- OUTER JOIN

- INNER JOIN은 WHERE 절에서부터 사용하던 JOIN의 DEFAULT 옵션으로/JOIN 조건에서 동일한 값이 있는 행만 반환한다. DEFAULT 옵션이므로 생략이 가능하지만, CROSS JOIN, OUTER JOIN과는 같이 사용할 수 없다
- NATURAL JOIN은 INNER JOIN의 하위 개념이므로 NATURAL INNER JOIN이라고 표시할 수 있으며, 결과는 NATURAL JOIN과 같다
- 새로운 SQL JOIN 문장 중에서 가장 중요하게 기억해야 하는 문장은 ON 조건절을 사용하는 경우이다. 과거 WHERE 절에서 JOIN 조건과 데이터 검증 조건이 같이 사용되어 용도가 불분명한 경우가 발생할 수 있었는데, WHERE 절의 JOIN 조건을 FROM절의 ON 조건절로 분리하여 표시함으로써 사용자가 이해하기 쉽도록 한다
- ON 조건절의 경우 NATURAL JOIN처럼 JOIN 조건이 숨어 있지 않고, 명시적으로 JOIN 조건을 구분할 수 있고, NATURAL JOIN이나 USING 조건절처럼 칼럼명이 똑같아야 된다는 제약없이 칼럼명이 상호 다르더라도 JOIN 조건으로 사용할 수 있으므로 앞으로 가장 많이 사용될 것으로 예상된다. 다만, FROM 절에 테이블이 많이 사용될 경우 다소 복잡하게 보여 가독성이 떨어지는 단점이 있다
- 그런 측면에서 SQL Server의 경우 ON 조건절만 지원하고 NATURAL JOIN과 USING 조건절을 지원하지 않고 있는 것으로 보인다. 본 교재는 ANSI/ISO-SQL 기준에 NATURAL JOIN과 USING 조건절이 표시되어 있으므로 이부분도 설명을 하도록 한다

**INNER JOIN**

- INNER JOIN은 OUTER JOIN과 대비하여 내부 JOIN이라고 하며 JOIN 조건에서 동일한 값이 있는 행만 반환한다
- INNER JOIN 표시는 그 동안 WHERE 절에서 사용하던 JOIN 조건을 FROM 절에서 정의하겠다는 표시이므로 USING 조건절이나 ON 조건절을 필수적으로 사용해야 한다
- ![스크린샷 2023-11-07 오후 5.30.00](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.30.00.png)

**NATURAL JOIN**

- NATURAL JOIN은 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI(=) JOIN을 수행한다
- NATURAL JOIN이 명시되었으면, 추가로 USING 조건절, ON 조건절, WHERE 절에서 JOIN 조건을 정의할 수 없다
- ![스크린샷 2023-11-07 오후 5.31.39](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.31.39.png)
- 별도의 JOIN 칼럼을 지정하지 않았지만, 두 개의 테이블에서 DEPTNO 라는 공통된 칼럼을 자동으로 인식하여 JOIN을 처리한 것이다. JOIN에 사용된 칼럼들은 같은 데이터 유형이어야 하며, ALIAS나 테이블 명과 같은 접두사를 붙일 수 없다
- NATURAL JOIN은 JOIN이 되는 테이블의 데이터 성격(도메인)과 칼럼명 등이 동일해야 하는 제약 조건이 있다. 간혹 모델링 상의 부주의로 인해 동일한 칼럼명이더라도 다른 용도의 데이터를 저장하는 경우도 있으므로 주의해서 사용해야 한다

**USING 조건절**

- NATURAL JOIN에서는 모든 일치되는 칼럼들에 대해 JOIN이 이루어지지만, FROM 절의 USING 조건절을 이용하면 같은 이름을 가진 칼럼들 중에서 원하는 칼럼에 대해서만 선택적으로 EQUI JOIN을 할 수가 있다
- ![스크린샷 2023-11-07 오후 5.39.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.39.14.png)
- USING 조건절을 이용한 EQUI JOIN에서도 NATURAL JOIN과 마찬가지로 JOIN에 사용된 칼럼들은 같은 데ㅣ터 유형이어야 하며, ALIAS나 테이블 명과 같은 접두사를 붙일 수 없다.

**ON 조건절**

- JOIN 서술부(ON 조건절)와 비 JOIN 서술부(WHERE 조건절)를 분리하여 이해가 쉬우며, 칼럼명이 다르더라도 JOIN 조건을 사용할 수 있는 장점이 있다.(대부분의 DBMS가 지원)
- ![스크린샷 2023-11-07 오후 5.40.43](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.40.43.png)
- 임의의 JOIN 조건을 지정하거나, 이름이 다른 칼럼명을 JOIN 조건으로 사용하거나, JOIN 칼럼을 명시하기 위해서는 ON 조건절을 사용한다. ON 조건절에 사용된 괄호는 옵션 사항이다
- ON 조건절과 WHERE 검색 조건은 충돌 없이 사용할 수 있다
- ![스크린샷 2023-11-07 오후 5.42.25](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.42.25.png)
- WHERE 절의 JOIN 조건과 같은 기능을 하면서도, 명시적으로 JOIN의 조건을 구분할 수 있으므로 가장 많이 사용될 것으로 예상된다. 다만, FROM 절에 테이블이 많이 사용될 경우 다소 복잡하게 보여 가독성이 떨어지는 단점이 있다
- ![스크린샷 2023-11-07 오후 5.43.08](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.43.08.png)
- ![스크린샷 2023-11-07 오후 5.43.19](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.43.19.png)
- ![스크린샷 2023-11-07 오후 5.43.35](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.43.35.png)

**CROSS JOIN**

- CROSS JOIN은 E.F.CODD 박사가 언급한 일반 집합 연산자의 PRODUCT의 개념으로 테이블 간 JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합을 말한다
- CARTESIAN PRODUCT 또는 CROSS PRODUCT와 같은 표현으로, 결과는 양쪽 집합의 M*N rjsdml epdlxj whgkqdl qkftodgksek
- 정상적인 데이터 모델이라면 CROSS PRODUCT 가 필요한 경우는 많지 않지만, 간혹 튜닝이나 리포트를 작성하기 위해 고의적으로 사용하는 경우가 있을 수 있다
- 데이터웨어하우스의 개별 DIMENSION(차원)을 FACT(사실) 칼럼과 JOIN하기 전에 모든 DIMENSION의 CROSS PRODUCT를 먼저 구할 때 유용하게 사용할 수 있다
- ![스크린샷 2023-11-07 오후 5.46.08](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.46.08.png)
- 56건의 결과 데이터는 EMP 14건 * DEPT 4건의 데이터 조합 건수이다

**OUTER JOIN**

- INNER JOIN과 대비하여 외부 JOIN이라고 불리며, JOIN 조건에서 동일한 값이 없는 행도 반환할 때 사용할 수 있다
- ![스크린샷 2023-11-07 오후 5.57.15](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 5.57.15.png)
- STANDARD JOIN을 사용함으로써 OUTER JOIN의 많은 문제점을 해결할 수 있고, 대부분의 관계형 DBMS 간에 호환성을 확보할 수 있으므로 명시적인 OUTER JOIN을 사용할 것을 적극적으로 권장한다
- 추가로 OUTER JOIN 역시 JOIN 조건을 FROM 절에서 정의하겠따는 표시이므로 USING 조건절이나 ON 조건절을 필수적으로 사용해야 한다
- LEFT/RIGHT OUTER JOIN의 경우에는 기준이 되는 테이블이 조인 수행시 무조건 드라이빙 테이블이 된다. 옵티마이저는 이 원칙에 위배되는 다른 실행계획을 고려하지 않는다. SQL 성능 저하의 원인이 될 수 있으므로 필요한 경우만 OUTER 조인을 사용해야 한다

**LEFT OUTER JOIN**

- 조인 수행시 먼저 표기된 좌측 테이블에 해당하는 데이터를 모두 읽은 후, 나중 표기된 우측 테이블에서 JOIN 대상 데이터를 읽어온다
- 우측 테이블의 JOIN 칼럼에서 JOIN 조건 값이 없는 경우에는 우측 테이블에서 가져오는 칼럼들은 NULL 값으로 채운다
- LEFT JOIN으로 OUTER 키워드를 생략해서 사용할 수 있다
- ![스크린샷 2023-11-07 오후 6.00.13](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 6.00.13.png)

**RIGHT OUTER JOIN**

- 조인 수행시 좌측, 우측 테이블의 모든 데이터를 읽어 OUTER JOIN하여 결과를 생성한다
- 즉, TABLE A와 B가 있을 때(TABLE 'A', 'B' 모두 기준이 됨), RIGHT OUTER JOIN과 LEFT OUTER JOIN의 결과를 합집합으로 처리한 결과와 동일하다
- 단, UNION ALL이 아닌 UNION 기능과 같으므로 중복되는 데이터는 삭제한다
- FULL JOIN으로 OUTER 키워드를 생략해서 사용할 수 있다
- ![스크린샷 2023-11-07 오후 6.01.49](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 6.01.49.png)

**INNER vs OUTER vs CROSS JOIN 비교**

![스크린샷 2023-11-07 오후 6.01.59](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-07 오후 6.01.59.png)

- 첫번째, INNER JOIN의 결과는 다음과 같다
  - 양쪽 테이블에 모두 존재하는 키 값이 B-B, C-C 인 2건이 출력된다
- 두번째, LEFT OUTER JOIN의 결과는 다음과 같다
  - TAB1를 기준으로 키 값 조합이 B-B, C-C, D-NULL, E-NULL 인 4건이 출력된다
- 세번째, RIGHT OUTER JOIN의 결과는 다음과 같다
  - TAB2를 기준으로 키 값 조합이 NULL-A, B-B, C-C 인 3건이 출력된다
- 네번째, FULL OUTER JOIN의 결과는 다음과 같다
  - 양쪽 테이블을 기준으로 키 값 조합이 NULL-A, B-B, C-C, D-NU::, E-NULL 인 5건이 출력된다
- 다섯번째, CROSS JOIN(CARTESIAN PRODUCT)의 결과는 다음과 같다
  - JOIN이 가능한 모든 경우의 수를 표시하지만, 단, OUTER JOIN은 제외한다
  - 양쪽 테이블 TAB1과 TAB2의 데이터를 곱한 개수인 4*3 =. 2건이 추출됨
  - 키 값 조합이 B-A, B-B, B-C, C-A, C-B, C-C, D-A, D-B, D-C, E-A, E-B, E-C 인 12건이 출력된다.