**FUNCTION**

- 함수는 다양한 기준으로 분류할 수 있는데, 벤더에서 제공하는 함수인 내장함수(Built-in FUNCTION)와 사용자가 정의할 수 있는 함수(User Defined FUNCTION)로도 나눌 수 있다.
- 내장 함수는 벤더별로 가장 큰 차이를 보이는 부분이지만, 핵심적인 기능들은 이름이나 사용법이 다르더라도 대부분의 데이터베이스가 공통적으로 제공하고 있다.
- <img src="/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.23.11.png" alt="스크린샷 2023-11-01 오후 5.23.11" style="zoom:150%;" />
- 일반적으로 함수는 입력되는 값이 많아도 출력은 하나만 된다는 M:1 관계라는 특징을 가지고 있다 (사용자 정의 함수의 경우 출력을 여러개 값이 나오게 할 수도 있다)
- 단일 행 함수의 경우 단일 행 내에 있는 하나의 값 또는 여러 값이 입력 인수로 표현될 수 있다.
- 단일 행 함수의 경우 각 행(Row)들에 대해 개별적으로 작용하여 데이터 값들을 조작하고, 각각의 행에 대한 조작 결과를 리턴한다.
- 단일 행 함수의 경우 SELECT, WHERE, ORDER BY 절에 사용 가능하다
- 특별한 제약이 없다면 함수의 인자(Arguments)로 함수를 사용하는 함수의 중첩이 가능하다
- ![스크린샷 2023-11-01 오후 5.25.21](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.25.21.png)
- ![스크린샷 2023-11-01 오후 5.25.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.25.33.png)

**문자형 함수**

- ![스크린샷 2023-11-01 오후 5.26.03](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.26.03.png)
- ![스크린샷 2023-11-01 오후 5.26.17](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.26.17.png)

**숫자형 함수**

- ![스크린샷 2023-11-01 오후 5.26.59](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.26.59.png)
- ![스크린샷 2023-11-01 오후 5.27.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.27.11.png)

**날짜형 함수**

- ![스크린샷 2023-11-01 오후 5.27.25](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.27.25.png)

**변환형 함수**

- 변환형 함수는 특정 데이터 타입을 다양한 형식으로 출력하고 싶을 경우에 사용되는 함수이다. 변환형 함수는 크게 두 가지 방식이 있다.
  - 명시적(Explicit) 데이터 유형 변환 : 데이터 변환형 함수로 데이터 유형을 변환하도록 명시해 주는 경우
  - 암시적(Implicit) 데이터 유형 변환 : 데이터베이스가 자동으로 데이터 유형을 변환하여 계산하는 경우
- 암시적 데이터 유형 변환의 경우 인덱스 미사용으로 인한 성능 저하가 발생할 수 있으며, 자동적으로 데이터베이스가 알아서 계산하지 않는 경우가 있어 에러를 발생할 수 있으므로 명시적인 데이터 유형 변환 방법을 사용하는 것이 바람직하다
- 명시적 데이터 유형 변환![스크린샷 2023-11-01 오후 5.52.51](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.52.51.png)
- ![스크린샷 2023-11-01 오후 5.53.33](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.53.33.png)
- ![스크린샷 2023-11-01 오후 5.53.42](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.53.42.png)

**CASE 표현**

- CASE 표현은 IF-THEN-ELSE 논리와 유사한 방식으로 표현식을 작성해서 SQL의 비교 연산 기능을 보완하는 역할을 한다
- ANSI-SQL 표준에는 CASE Expression이라고 표시되어 있는데, 함수와 같은 성격을 가지고 있으며 Oracle의 Decode 함수와 같은 기능을 하므로 단일행 내장 함수에서 같이 설명을 한다
- ![스크린샷 2023-11-01 오후 5.55.00](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.55.00.png)
- ![스크린샷 2023-11-01 오후 5.55.12](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.55.12.png)

**SIMPLE_CASE_EXPRESSION**

- SIMPLE_CASE_EXPRESSION은 CASE 다음에 바로 조건에 사용되는 칼럼이나 표현식을 표시하고, 다음 WHEN 절에서 앞에서 정의한 칼럼이나 표현식과 같은지 아닌지 판단하는 문장으로 EQUI(=) 조건만 사용한다면 SEARCHED_CASE_EXPRESSION보다 간단하게 사용할 수 있는 장점이 있다.
- Oracle의 DECODE 함수와 기능면에서 동일하다
- ![스크린샷 2023-11-01 오후 5.58.29](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 5.58.29.png)

**SEARCHED_CASE_EXPRESSION**

- SEARCHED_CASE_EXPRESSION은 CASE 다음에는 칼럼이나 표현식을 표시하지 않고, 다음 WHEN 절에서 EQUI(=) 조건 포함 여러 조건(>, >=, <, <=)을 이용한 조건절을 사용할 수 있기 때문에 SIMPLE_CASE_EXPRESSION보다 훨씬 다양한 조건을 적용할 수 있는 장점이 있다.
- ![스크린샷 2023-11-01 오후 6.00.06](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.00.06.png)

**CASE 중첩**

- CASE 표현은 함수의 성질을 가지고 있으므로, 다른 함수처럼 중첩해서 사용할 수 있다
- ![스크린샷 2023-11-01 오후 6.20.04](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.20.04.png)

**NULL 관련 함수**

- NULL 값을 포함하는 연산의 경우 결과 값도 NULL 값이다. 모르는 데이터에 숫자를 더하거나 빼도 결과는 마찬가지로 모르는 데이터인 것과 같다.
- 결과값을 NULL이 아닌 다른 값을 얻고자 할 때 NVL/ISNULL 함수를 사용한다. NULL 값의 대상이 숫자 유형 데이터인 경우는 주로 0으로, 문자 유형 데이터인 경우는 블랭크보다는 'x'같이 해당 시스템에서 의미 없는 문자로 바꾸는 경우가 많다
- ![스크린샷 2023-11-01 오후 6.21.57](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.21.57.png)
- ![스크린샷 2023-11-01 오후 6.46.13](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.46.13.png)
- ![스크린샷 2023-11-01 오후 6.46.23](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.46.23.png)

**NULL과 공집합**

- SELECT 1 FROM DUAL WHERE 1 = 2; 같은 조건이 대표적인 공집합을 발생시키는 쿼리이며, 위와 같이 조건에 맞는 데이터가 한 건도 없는 경우를 공집합이라고 하고, NULL 데이터와는 또 다르게 이해해야 한다.
- ![스크린샷 2023-11-01 오후 6.47.26](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.47.26.png)
- ![스크린샷 2023-11-01 오후 6.50.57](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.50.57.png)
- ![스크린샷 2023-11-01 오후 6.52.01](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.52.01.png)

**NULLIF**

- NULLIF 함수는 EXPR1이 EXPR2 와 같으면 NULL을, 같지 않으면 EXPR1을 리턴한다. 특정 값을 NULL로 대체하는 경우에 유용하게 사용할 수 있다
- ![스크린샷 2023-11-01 오후 6.54.11](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.54.11.png)

**COALESCE**

- COALESCE 함수는 인수의 숫자가 한정되어 있지 않으며, 임의의 개수 EXPR에서 NULL이 아닌 최초의 EXPR을 나타낸다. 만일 모든 EXPR이 NULL이라면 NULL을 리턴한다

- ![스크린샷 2023-11-01 오후 6.55.21](/Users/asthu/Library/Application Support/typora-user-images/스크린샷 2023-11-01 오후 6.55.21.png)

  



