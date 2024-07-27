**INSERT**

- 테이블에 데이터를 입력하는 방법은 두 가지 유형이 있으며 <u>한 번에 한 건만 입력된다</u>![스크린샷 2023-10-28 오후 5.13.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 5.13.14.png)
- 해당 칼럼의 데이터 유형이 CHAR나 VARCHAR2 등 문자 유형일 경우 ['] (SINGLE QUOTATION)로 입력할 값을 입력한다
- 숫자일 경우 ''을 붙이지 않아도 된다.

**INSERT (a type)**

- a 유형은 테이블의 칼럼을 정의할 수 있는데, 이때 칼럼의 순서는 테이블의 칼럼 순서와 매치할 필요는 없으며, 정의하지 않은 칼럼은 Default로 NULL값이 입력된다.
- 단, PK나 NOT NULL로 지정된 칼럼은 NULL이 허용되지 않는다.

**INSERT (b type)**

- b 유형은 모든 칼럼에 데이터를 입력하는 경우로 굳이 COLUMN_LIST를 언급하지 않아도 되지만, 칼럼의 순서대로 빠짐없이 데이터가 입력되어야 한다.
- 데이터를 입력하는 경우 정의되지 않은 미지의 값인 경우, ''(SINGLE QUOTATION)을 붙여서 표현하거나, NULL이라고 명시적으로 표현할 수 있다.

**UPDATE**

- UPDATE 다음에 수정되어야 할 칼럼이 존재하는 테이블명을 입력하고, SET 다음에 수정되어야 할 칼럼명과 해당 칼럼 수정값으로 변경이 이루어진다.![스크린샷 2023-10-28 오후 5.33.18](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 5.33.18.png)
- 일반적으로는 5절에서 배울 WHERE 절을 사용하여 UPDATE 대상 행을 선별한다. WHERE 절을 사용하지 않는다면 테이블의 전체 데이터가 수정된다.

**DELETE**

- DELETE FROM 다음에 삭제를 원하는 자료가 저장되어 있는 테이블명을 입력하고 실행한다. 이때 FROM 문구는 생략이 가능한 키워드이다. ![스크린샷 2023-10-28 오후 5.34.41](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 5.34.41.png)
- 일반적으로는 5절에서 배울 WHERE 절을 사용하여 DELETE 대상 행을 선별한다. WHERE 절을 사용하지 않는다면 테이블의 전체 데이터가 수정된다.

**SELECT**

- 조회하기를 원하는 칼럼명을 SELECT 다음에 콤마 구분자(,)로 구분하여 나열하고, FROM 다음에 해당 칼럼이 존재하는 테이블명을 입력하여 실행시킨다. ![스크린샷 2023-10-28 오후 5.35.42](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 5.35.42.png)

- 해당 테이블의 모든 칼럼 정보를 보고 싶을 경우에는 와일드 카드로 애스터리스크(*)를 사용하여 조회할 수 있다.![스크린샷 2023-10-28 오후 5.47.40](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 5.47.40.png)

- 실행 결과 화면을 보면 칼럼 레이블이 맨 위에 보여지고, 레이블 밑에 점선이 보여진다. 실질적인 자료는 다음 줄부터 시작된다.

- 레이블은 기본적으로 대문자로 보여지고, 첫 라인에 보여지는 레이블의 정렬은 다음과 같다. 

  좌측 정렬 : 문자 및 날짜 데이터, 우측정렬 : 숫자 데이터

**SELECT - ALIAS**

- 조회된 결과에 일종의 별명(ALIAS, ALIASES)을 부여해서 칼럼 레이블을 변경할 수 있다
- 칼럼명 바로 뒤에 온다
- 칼럼명과 ALIAS 사이에 AS, as 키워드를 사용할 수도 있다(option)![스크린샷 2023-10-28 오후 6.28.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 6.28.11.png)
- ALIAS 사용시 이중 인용부호(Double Quotation)는 ALIAS가 공백, 특수 문자를 포함할 경우와 대소문자 구분이 필요할 경우 사용된다.![스크린샷 2023-10-28 오후 6.32.57](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 6.32.57.png)

**SELECT - 산술 연산자**

- 산술 연산자는 NUMBER와 DATE 자료형에 대해 적용되며 일반적으로 수학에서의 4칙 연산과 동일하다
- 우선순위를 위한 괄호 적용이 가능하다
- 수학에서와 같이 (), *, /, +, - 의 우선 순위를 가진다
- 적절한 ALIAS를 새롭게 부여하는 것이 좋다![스크린샷 2023-10-28 오후 6.35.14](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 6.35.14.png)

**SELECT - 합성 연산자**

- 문자와 문자를 연결하는 합성(CONCATENATION) 연산자를 사용하면 별도의 프로그램 도움 없이도 SQL 문장만으로도 유용한 리포트를 출력할 수 있다. 합성(CONCATENATION) 연산자의 특징은 다음과 같다
- 문자와 문자를 연결하는 경우 2개의 수직 바(||)에 의해 이루어진다.(Oracle)
- 문자와 문자를 연결하는 경우 + 표시에 의해 이루어진다. (SQL Server)
- 두 벤더 모두 공통적으로 CONCAT(string1, string2) 함수를 사용할 수 있다.
- 칼럼과 문자 또는 다른 칼럼과 연결시킨다.
- 문자 표현식의 결과에 의해 새로운 칼럼을 생성한다
- ![스크린샷 2023-10-28 오후 6.38.43](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 6.38.43.png)
- ![스크린샷 2023-10-28 오후 6.39.08](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-10-28 오후 6.39.08.png)

**DUAL 테이블**

- Oracle은 SELECT 절과 FROM 절 두개의 절이 SELECT SQL 문장의 필수 절로 지정되어 있으므로, 사용자 테이블이 필요 없는 SQL 문장의 경우에도 필수적으로 DUAL이라는 테이블을 FROM 절에 지정한다
- 특성
  - 사용자 SYS가 소유하며 모든 사용자가 액세스 가능한 테이블이다
  - SELECT ~ FROM ~ 의 형식을 갖추기 위한 일종의 DUMMY 테이블이다
  - DUMMY 라는 문자열 유형 칼럼에 'X'라는 값이 들어 있는 행을 1건 포함하고 있다
- 반면 사이베이스(Sybase)나 MS SQL Server의 경우에는 SELECT 절만으로도 SQL 문장이 수행 가능하도록 정의하였기 때문에 DUAL 이란 DUMMY 테이블이 필요 없다. 물론 사이베이스나 MS SQL Server의 경우에도 사용자 테이블의 칼럼을 사용할 때는 FROM 절이 필수적으로 사용되어야 한다