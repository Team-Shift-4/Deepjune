## SELECT

---

> ♣︎ 기본 SELECT 문의 구문

- 표시할 열을 지정하기 위한 SELECT 절
- 데이터가 저장된 테이블을 지정하는 FROM 절
- 구문

```
SELECT * | {[DISTINCT] column | 표현식 [별칭],...}
FROM table;
```

<br>

> ♣︎ SELECT 절의 열 선택

- 모든 열 선택

  - SELECT 뒤에 \*를 사용하여 테이블에 있는 데이터의 모든 열을 표시
  - SELECT 절에 테이블의 모든 열을 지정하는 방법을 대체
    <br>

- 특정 열의 선택
  - 열 이름을 쉼표로 구분하여 지정
  - SELECT 절에 출력 결과로 표시할 순서대로 열을 지정

<pre><code>
SELECT *
FROM y_dept;

SELECT dept_id, dept_name, loc_id, mgr_id
FROM y_dept;
</code></pre>

두 실행문의 결과는 `y_dept`의 테이블의 모든 열에 모든 행을 표시

> ♣︎ 중복행의 제거[DISTINCT]

- SELECT의 결과는 기본적으로 중복 행을 제거하지 않은 상태로 결과를 표시
  - 결과에서 중복 행을 제거하려면 SELECT 절에 DISTINCT 키워드를 사용
- DISTINCT는 SELECT 절에 한 번만 사용 가능
- DISTINCT 다음에 여러 열을 지정하면 결과에는 열 조합 값에 대해 중복을 제거하고 표시

<pre><code>
SELECT dept_id
FROM y_emp; // y_emp 테이블의 모든 부서번호를 출력

SELECT DSTINCT dept_id
FROM y_emp; / y_emp 테이블의 모든 사원의 부서번호를 중복을 제거하고 출력
</code></pre>

> ♣︎ 산술식의 사용

- 산술연산자를 사용하여 숫자 및 날짜 데이터에 대한 표현식을 작성

  - FROM 절을 제외한 SQL 문의 모든 절에서 산술 연산자 사용 가능
  - 산술연산자의 종류 : +, -, \*, /
    <br>

- 산술식 안에 여러 연산자가 있을 경우
  - 곱셈과 나눗셈 우선
  - 우선순위가 동일한 연산자는 왼쪽에서 오른쪽으로 계산
  - 괄호를 사용하여 우선순위가 조정

<pre><code>
SELECT emp_id, emp_name, salary, salary+300
FROM y_emp; // 출력 결과에 급여가 300 인상된 급여를 salary+300으로 표시

SELECT emp_name, salary, 12*(salary+300)
FROM y_emp; // 괄호를 사용하여 연산자의 실행 순서를 바꿀수있다.
</code></pre>

> ♣︎ 날짜 데이터의 연산

- 날짜 데이터에 산술연산자를 사용하여 정수를 더하거나 빼기 가능

  - 한 날짜에서 다른 날짜 빼서 날짜 간의 일 수 계산
  - 계산 과정 또는 결과의 정수를 일 수에 해당
    <br>

- SYSDATE 함수

  - 현재의 날짜를 결과로 반환하는 오라클 제공의 내장함수
    <br>

- DUAL 테이블
  - 오라클에서 제공하는 DUMMY 테이블
  - 단일 열과 단일 행으로 구성
  - 주로 함수의 결과나 산술연산, 날짜연산의 결과를 표시하기 위하여 사용

```
SELECT SYSDATE
FROM dual; // 내장 함수인 SYSDATE를 사용하여 현재의 날짜를 표시

SELECT emp_id, hiredate, hiredate+30
FROM y_emp; // 사원의 입사일과 입사일로부터 30일 후의 날짜를 사원번호와 함께 출력
```

> ♣︎ NULL 값의 사용과 산술식

- 알 수 없는 값, 사용할 수 없는 값, 할당할 수 없는 값, 적용할 수 없는 값을 의미
- 0이나 공백과 구분
  - 0은 숫자이고 공백은 하나의 문자
- **산술식 NULL값이 사용되면 산술식의 결과 또한 NULL**

```
SELECT emp_id, emp_name, comm
FROM y_emp; // y_emp 테이블의 comm 열은 커미션을 받은 일부 사원을 제외한 대부분의 사원이 NULL 값을 저장하고있다

SELECT emp_id, salary, comm, (salary*12) + (salary*comm)
FROM y_emp; // 사원의 연봉을 계산한다면 commm이 NULL인 사원은 연봉이 NULL이 된다
```

> ♣︎ 열 머리글과 열 별칭

- SELECT문의 결과에서 열의 머리글

  - 기본적으로 대문자로 표시
  - 표현식에 의해 생성된 열은 표현식 자체가 열의 이름으로 사용
    <br>

- 열 별칭(alias)

  - SELECT 절에서 열 이름이나 표현식 대신 사용
  - 출력결과를 이해하기 쉽도록(Readability)하기 위해 열의 이름이나 표현식을 다른 이름으로 변경
    <br>

- 열 별칭 사용법
  - SELECT 목록에서 열 이름 또는 표현식과 별칭 사이에 공백 또는 AS를 넣어 지정
  - 대문자 표시가 기본
  - 별칭을 큰 따옴표(" ")로 묶는 경우
    - 별칭이 공백 또는 특수 문자를 포함하는 경우
    - 대소문자를 구분할 경우

```
SELECT emp_name Name, comm AS commission, salary * 12 "Annual Salary"
FROM y_emp;
```

> ♣︎ 연결연산자[||]와 Q연산자

- 하나 이상의 열 또는 표현식을 결합하여 결과에 하나의 열로 표시
- 연산자의 종류
  - 연결연산자(||)
  - Q연산자
- 임의의 리터럴과 함께 사용하여 의미있는 출력결과 생성

```
SELECT emp_name || position AS "Employee's Position"
FROM y_emp; // {송강호사장} 출력

SELECT emp_name || ' ' || position AS "Employee's Position"
FROM y_emp; // {송강호 사장} 출력

SELECT emp_name || '''s Salary : ' || salary AS "Employee's Salary"
FROM y_emp; // {송강호's Salary : 930} 출력

SELECT emp_name || q'['s Salary : ]' || salary AS "Employee's Salary"
FROM y_emp; // {송강호's Salary : 930} 출력
```

> ♣︎ 문장 작성법과 기능

- SQL 문의 작성의 규칙과 지침
  - SQL 문은 대소문자를 구분하지 않음
    - 키워드는 대문자로 입력하고 테이블 이름, 열 등은 소문자로 입력하는 것이 일반적
- SQL 문은 하나 이상의 줄에 입력할 수 있으며 종료문자(;)를 입력하여 명령문을 완료하고 실행
- 키워드는 줄간 나눠 쓰거나 약어로 쓸 수 없음
- 절은 읽기 쉽고 편집하기 쉽도록 서로 다른 줄에 쓰도록 권장
- 좀 더 읽기 쉬운 SQL 문을 작성하기 위해 들여쓰기를 사용
  <br>

> ♣︎ SELECT 문의 기능

- Projection
  - 열을 선택하여 SELECT 하는 기능
- Selection
  - 조건문을 사용하여 표시할 행을 제한하는 기능
- Join
  - 둘 이상의 테이블을 연결하여 단일 결과로 조합하여 출력하는 기능
    <br>

### WHERE 절의 사용

- WHERE 절을 사용하여 쿼리에 반환되는 행을 제한
  - FROM 절 다음에서 조건을 표현하기 위해 열 이름, 표현식, 비교 연산자 및 상수로 구성
  - 단일 SELECT 문장에서 WHERE 절은 한 번만 사용 가능
    - WHERE 절에 여러 조건을 지정하기 위하여 AND, OR과 같은 논리 연산자를 사용
- 구문

```
SELECT * | {[DISTINCT] column | 표현식 [별칭],...}
FROM table
WHERE 조건;
```

> ♣︎ WHERE 절의 기본 사용법

- 열 이름, 비교 조건, 상수 또는 값 목록 등 세 가지 요소로 구성
- 문자열 및 날짜는 단일 인용부호로 묶어야 하며 대소문자 구분
- 날짜는 기본 날짜 형식을 사용

```
SELECT emp_id, emp_name, position, dept_id
FROM y_emp
WHERE dept_id = 100; // dept_id가 100인 사원 출력

SELECT emp_id, emp_name, position, dept_id
FROM y_emp
WHERE position = '부사장'; // 직급이 부사장인 사원 출력

SELECT emp_id, emp_name, salary, hiredate
FROM y_emp
WHERE hiredate = '01/03/19'; // hiredate가 01/03/19 인 사원 출력
```

> ♣︎ 인반 비교연산자

- 주로 표현식을 다른 값이나 표현식과 대소비교를 하기 위해 사용
- 일반적인 비교연산자의 종류
<p align="center"><img src="./img/Select%20Grammar/비교연산자.png" width="630" height="300" /></p>

```
SELECT emp_id, emp_name, salary
FROM y_emp
WHERE salary <= 400; // y_emp테이블에서 급여가 400 이하인 사원 출력

SELECT emp_name, salary*12 annsal
FROM y_emp
WHERE salary * 12 > 8000; // 연봉이 8000보다 많은 직원을 검색
```

> ♣︎ 기타 SQL 연산자

- SQL에서만 사용되는 비교연산자
- 모든 데이터 유형에 적용
- SQL 연산자의 종류
<p align="center"><img src="./img/Select%20Grammar/기타%20비교연산자.png" width="630" height="200" /></p>

- BETWEEN ... AND ...
  - BETWEEN 범위 조건을 사용하면 값의 범위에 따라 행을 표시
  - 하한값과 상한값도 지정된 범위에 포함
  - BETWEEN 조건으로 지정한 값은 하한값을 먼저 지정
- IN(list...)
  - IN 연산자 다음의 괄호 안에 원하는 값의 리스트를 명시
  - 리스트에 포함된 값중 하나와 일치되는값을 포함하는 행히 결과로 반환

```
SELECT emp_name, slary
FROM y_emp
WHERE salary BETWEEN 600 AND 700; // 급여가 600 이상이고 700이하인 사원을 출력

SELECT emp_id, emp_name, salary, mgr_id
FROM y_emp
WHERE mgr_id IN(1001,1002,1003); // 관리자의 사원 번호가 1001~1003인 모든 사원 출력

SELECT emp_name, position, dept_id
FROM y_emp
WHERE position IN ('부장','차장'); // 직급이 부장, 차장인 사원 출력
```

> ♣︎LIKE

- 검색할 값을 정확하게 알지 못하는 경우 LIKE조건을 사용하여 문자 패턴이 일치하는 행을 선택
- 검색 문자열은 % 또는 \_, 이 두 가지 기호를 사용하여 구성
  - %는 0개 이상의 문자 대체
  - \_는 하나의 문자만 대체
- %나 \_가 포함된 데이터의 검색 방법
  - %나 \_ 앞에 ESCAPE 문자로 지정
  - ESCAPE 문자는 사용자 임의로 지정 가능

```
SELECT emp_id, emp_name
FROM y_emp
WHERE emp_name LIKE '김%'; emp_name이 김씨인 사원 출력

SELECT emp_id, emp_name
FROM y_emp
WHERE emp_naem LIKE '_승%'; // 이름의 두 번째 문자가 '승'인 사원을 출력

SELECT *
FROM pay_grade
WHERE pay_level LIKE '%\_B' ESCAPE '\'; // pay_level이 "_B"인 정보 출력

SELECT emp_name, hiredate
FROM y_emp
WHERE hiredate LIKE '07%'; // 2007년도에 입사한 모든 사원 출력
```

> ♣︎ NULL 조건

- NULL 값은 어떤 값과도 동일성 여부를 판별 불가
  - = NULL은 사용하여 비교불가능
  - NULL 여부를 테스트하기 위한 비교연산자를 사용
  - NULL인 데이터를 보기 위해서 IS NULL 연산자를 사용
  - NULL이 아닌 데이터를 조회하기 위해서는 IS NOT NULL 연산자를 사용.

```
SELECT emp_id, emp_name, position, dept_id
FROM y_emp
WHERE dept_id IS NULL; // 부서정보가 NULL인 사원 출력

SELECT emp_id, emp_name, comm
FROM y_emp
WHERE comm IS NOT NULL; // COMM이 NULL이 아닌 사원 출력
```

> ♣︎ 논리 연산자[AND, OR, NOT]

- 단일 SELECT 문에 WHERE 절은 한 번만 사용
- WHERE 절에 여러 조건을 조합하여 출ㄹㄱ될 행을 더욱더 제한하기 위하여 논리연산자를 사용
- 논리연산자의 종류

  - AND
  - OR
  - NOT

- AND 연산자
  - WHERE 절의 조건을 모두 만족하는 데이터를 반환
  - 조건가운데 어느 한 가지 조건에 대한 결과라도 거짓 또는 NULL 일경우 해당 행은 결과에 포함되지 않는다.
- OR 연산자
  - OR 연산자는 조건 중 하나만 만족하면 레코드를 선택
  - 조건가운데 어느 한 가지 조건에 대한 결과가 거짓 또는 NULL일 경우에도 해당 행은 결과에 포함된다.
- NOT 연산자
  - NOT 연산자 다음에 오는 조건에 대해 거짓인 행이 반환
  - NOT 연산자는 BTWEEN, LIKE, IN 등 다른 SQL 연산자와 함께 사용
- NOT 연산자의 사용예시
  - NOT IN
  - NOT LIKE
  - NOT BETWEEN
  - IS NOT NULL

```
SELECT emp_id, emp_name, position, dept_id
FROM y_emp
WHERE position = '사원' AND
      dept_id = 400; // 직급이 '사원'이고 400번 부서에 속하는 사원 출력

SELECT emp_id. emp_name, position, dept_id
FROM y_emp
WHERE position = '사원' OR
      dept_id = 400; // 직급이 '사원'이거나 400번 부서에 속하는 사원 출력

SELECT emp_id, position, dept_id
FROM y_emp
WHERE position NOT IN('과장','대리','사원'); // 직급이 과장,대리,사원이 아닌 사원 출력
```

> ♣︎ 연산자 우선 순위 규칙

- 표현식을 평가하고 계산하는 순서를 결정
- 괄호를 사용하여 우선순위 변경가능
- 기본 우선순위 순서
<p><img src="./img/Select%20Grammar/연산자우선순위.png" width="350" height="200" /></p>

```
SELECT emp_name, position, salary
FROM y_emp
WHERE position = '차장' OR
      position = '부장' AND
      salary > 700; // 직급이 차장 이거나 부장이고 급여가 700이 넘는 사원 출력

SELECT emp_name, position, salary
FROM y_emp
WHERE(position = '차장' OR position = '부장') AND
      salary > 700; // 차장 또는 부장인 사원 가운데 급여가 700이 넘는 사원 출력
```

### 데이터 정렬

> ♣︎ ORDER BY

- ORDER BY 절을 사용하여 특정 순서로 행을 표시

```
SELECT *|{[DISTINCT] column|표현식 [별칭],...}
FROM table
[WHERE 조건(s)]
[ORDER BY {column, 표현식}[ASC|DESC]];
```

- SQL 문의 가장 끝에 위치
- 행을 오름차순(기본 순서) 또는 내림차순으로 정렬
  - 선택적으로 [ASC|DESC] 지정

> ♣︎ 출력 데이터의 정렬 방식

- 여러 열 기준의 정렬
  - ORDER BY 절에 쉼표로 열 이름을 구분하면서 여러 열을 지정
  - 결과는 첫 번째 열 기준으로 정렬된 다음 그 결과 내에서 두 번째 열을 기준으로 정렬하는 방식
  - ASC, DESC는 열 이름마다 별도 지정
- ORDER BY 절에 지정가능한 정렬 조건
  - 열이름 또는 표현식
  - 별칭
  - SELECT 절에 나열된열 목록을 기준으로 한 열 위치 값

```
SELECT emp_name, position, dept_id, hiredate
FROM y_emp
ORDER BY hiredate; // 입사일이 가장 빠른 순서부터 오름차순으로 테이블을 출력

SELECT emp_name, position, dept_id, hiredate
FROM y_emp
ORDER BY hiredate DESC; // 입사일이 가장 늦은 순서부터 내림차순으로 테이블 출력

SELECT emp_id, emp_name, dept_id, salary
FROM y_emp
ORDER BY dept_id, salary DESC; // 부서번호 기준으로 오름차순 하고 급여가 많은 순서대로 내림차순 출력

SELECT emp_id, emp_name, salary * 12 annsal
FROM y_emp
ORDER BY annsal DESC; // 연봉 * 12 기준으로 내림차순으로 정렬

SELECT emp_id, emp_name, salary * 12 annsal
FROM y_emp
ORDER BY 3 DESC; // 연봉 * 12 기준으로 내림차순으로 정렬(별칭으로도 가능)
```
