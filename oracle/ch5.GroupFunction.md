### 그룹함수

---

> ♣︎ 그룹함수의 개념

- 행 집합에 작용하여그룹 당 하나의 결과를 생성
- 행 집합은 테이블 전체 혹은 WHERE 절의 조건에 의해 선택된 행들이 하나의 그룹
- 구문

```
SELECT group_function(column), ...
FROM table
[ WHERE 조건(s) ];
```

- 선택된 행들에 대하여 하나의 그룹으로 처리되기 때문에 그룹 함수의 결과는 항상 단일 행

<br>

> ♣︎ 그룹함수의 종류

- 데이터베이스 관련 실무에서 전체 데이터에 대한 총계, 평균, 표준편차와 같은 통계 데이터를 결과로 출력하기 위하여 사용하는 강력한 SQL 기능
  <br>

- SQL에서 사용 가능한 그룹함수의 종류

  - COUNT
  - MIN
  - MAX
  - AVG
  - SUM

- SUM, AVG 함수

  - 숫자 데이터를 저장하는 열에 대해 선택된 데이터들의 합계와 평균을 구함
  - SUM(합계), AVG(평균)
    <br>

- MIN, MAX 함수

  - 모든 데이터 타입에 사용 가능(날짜 타입에도 사용 가능)
  - 선택된 열에 대한 최소값, 최대값을 구함
  - MIN(최소값), MAX(최대값)
    <br>

- COUNT 함수

  - 행의 개수를 반환하는 함수로 세 가지 표현식이 가능 - COUNT(\*) - NULL 값이 있는 행 및 중복 행을 포함 - 테이블에서 SELECT 문의 WHERE 조건을 만족하는 행 수를 반환 - COUNT(expr) - 열에 NULL이 아닌 행 수를 반환 - COUNT(DISTINCT expr) - expr로 식별되는 열에서 중복되지 않는 NULL이 아닌 값의 수를 반환
    <br>

- 그룹함수와 널값
  - COUNT(\*)를 제외한 그룹함수의 결과에 널값은 제외
  - 널값이 포함된 행을 그룹함수 결과에 포함하기 위해 NVL함수 사용
  - 예시 - AVG(comm), AVG(NVL(comm, 0))

```
SELECT SUM(salary), AVG(salary), MAX(salary), MIN(salary)
FROM y_emp; // salary의 합계, 평균, 최대값, 최소값 출력

SELECT MIN(hiredate), MAX(hiredate)
FROM y_emp; // 가장 늦게 입사한 사원과 가장 최근에 입사한 사원 출력

SELECT COUNT(*), COUNT(dept_id), COUNT(DISTINCT dept_id)
FROM y_emp; // 출력결과 : 33, 32, 4 총사원수는 33명이지만 부서가 NULL인 사원이 1명 있기떄문에 중간 결과는 32명이 출력

SELECT AVG(NVL(comm, 0)), AVG(comm)
FROM y_emp; // 첫번째 평균은 테이블의 모든 행을 기반으로 계산, 두번째 평균은 커미션을 받는 사원들만의 평균
```

<br>

> ♣︎ GROUP BY와 그룹 결과의 정렬

- 그룹 함수를 사용하는 쿼리문에 GROUP BY 절을 추가
  - 선택된 행을 서브그룹으로 나눈 후 그룹 함수를 사용하여 각 서브그룹에 대한 집계정보를 산출
  - GROUP BY 절에는 서브그룹(소그룹)의 기준 열의 이름을 명시
- 구문

```
SELECT column, group_function(column), ...
FROM table
[ WHERE 조건(s) ]
GROUP BY group_by _표현식
ORDER BY column;
```

<br>

> ♣︎ GROUP BY 절의 기본적인 사용법

- FROM 절 다음에 GROUP BY 절을 명시
- 서브그룹 생성 전에 제외할 행이 있다면 GROUP BY 절보다 앞에 WHERE 절에 지정
- GROUP BY 절에 지정되는 열 이름만 SELECT 절에 지정 가능
  <br>

- 여러 열 기준의 서브 그룹
  - 그룹 내 그룹에 대한 결과를 확인해야 할 경우
    - 각 부서 내에서 업무별로 지급되는 급여 총액을 표시하는 보고서를 작성해야 하는 경우
  - GROUP BY 절에 하나 이상의 열을 나열하여 최하위 서브 그룹에 대한 요약 결과를 반환
  - GROUP BY 절에 지정하는 열의 순서에 따라 상이한 결과 반환
    - 예시
      - GROUP BY dept_id, position
      - GROUP BY position, dept_id

```
SELECT dept_id, COUNT(*), SUM(salary), AVG(salary)
FROM y_emp
GROUP BY dept_id; // 각 부서의 사원수가 몇명 있는지, 그 사원수의 급여총합, 평균을 출력

SELECT dept_id, position, SUM(salary)
FROM y_emp
GROUP BY dept_id, position
ORDER BY dept_id; // 각 부서별 직급별 급여의 총 합을 반환하고 부서번호 기준으로 오름차순 정렬 후 출력
```

<br>

### 그룹결과의 제한과 그룹 합수의 중첩

> ♣︎ HAVING 절의 사용

- 그룹화된 결과를 제한하기 위해 HAVING 절 사용
  - 예 : 부서별 총급여를 구한 후 총급여가 3000이상인 부서만 표시
  - WHERE 절 : 선택할 행을 제한
  - HAVING 절 : GROUP BY 절과 함께 사용하여 그룹을 제한
- 구문

```
SELECT column, group_function(column), ...
FROM table
[ WHERE 조건(s) ]
GROUP BY group_by _표현식
HAVING group_조건
ORDER BY column;
```

<br>

> ♣︎ 그룹함수의 중첩

- 그룹 함수끼리의 중첩은 두 번까지만 가능
  - 참고 : SQL 함수의 중첩레벨에는 제한이 없음
- 그룹 함수가 중첩되어 사용되는 경우에 SELECT 절에 다른열 이름을 사용 불가
  - 예시 : SELECT dept_id, MAX(AVG(salary)) FROM y_emp GROUP BY dept_id;

```
SELECT dept_id, MAX(salary), MIN(salary)
FROM y_emp
GROUP BY dept_id
HAVING AVG(salary) > 600; // 평균급여가 700이 넘는 부서들의 최고와 최저급여 출력

SELECT MAX(COUNT(*)), MIN(COUNT(*))
FROM y_emp
GROUP BY dept_id; // 사원이 가장 많은 부서와 가장 적은 부서의 인원수를 출력
```

### GROUP BY 절의 추가 기능

> ♣︎ GROUP BY 절의 추가 연산자

- GROUP BY 절에 두 개 이상의 열을 지정하는 경우 그룹함수는 항상 가장 마지막 소그룹에 대한 결과만 반환
- GROUP BY 절에 연산자를 추가하여 하나의 쿼리문 안에서 여러 차원의 그룹화 연산 가능
- GROUP BY 절의 추가 연산자 종류
  - ROLLUP 연산자
  - CUBE 연산자
  - GROUPING SETS 연산자

<br>

> ♣︎ ROLLUP 연산자

- 정규 GROUP BY에 의한 그룹화 행과 하위 총계(중간소계, Sub-Total) 값을 포함하는 결과 집합을 산출
  - 기존 GROUP BY 절에 지정된 그룹화 목록에 따라 가장 하위 레벨부터 시작하여 최상위 총계까지 차례로 계산
  - 엑셀(전자스프레드시트)에서의 부분합을 구하는 작업과 유사
- 보고서 작성 시 결과 집합에서 통계 및 요약 정보를 추출하는 데 유용하게 사용
  <br>

- GROUP BY 절에 연산자 추가
- 그룹은 괄호 안에 표시
- 구문

```
SELECT [column,] group_function(column_name). . .
FROM table
[WHERE 조건(s)]
GROUP BY ROLLUP group_by_표현식
[HAVING having_표현식];
[ORDER BY column_name];
```

- ROLLUP 연산자 사용 예시
  - GROUP BY ROLLUP(dept_id, position)에는 다음의 결과 표시
    - GROUP BY dept_id, position
    - GROUP BY dept_id
    - GROUP BY 하지 않은 결과
  - 총계와 함께 하위 총계(소계)를 산출하는 데 유용
    <br>

> ♣︎ CUBE 연산자

- ROLLUP과 함께 SELECT 문의 GROUP BY 절에 사용할 수 있는 기능
  - 일반적으로 하나의 SELECT 문으로 교차 표 형식 보고서(cross tabulation)에 사용되는 결과 집합을 산출하기 위하여 사용
- GROUP BY 절에 지정된 모든 그룹의 조합에 대해 하위 총계와 최상위 총계를 모두 산출
  - GROUP BY 절에 있는 열 또는 표현식의 모든 조합이 상위 집계를 산출하는데 사용
  - ROLLUP 결과 집합을 포함하여 추가 행 생성
- 구문

```
SELECT [column,] group_function(column_name). . .
FROM table
[WHERE 조건(s)]
GROUP BY CUBE group_by_표현식
[HAVING having_표현식];
[ORDER BY column_name];
```

- CUBE 연산자 사용 예시
  - GROUP BY CUBE(dept_id, position)에는 다음의 결과가 함께 표시 - GROUP BY dept_id, position - GROUP BY dept_id - GROUP BY position - GROUP BY 하지 않은 결과
    <br>

> ♣︎ GROUPING 함수

- ROLLUP과 CUBE 연산자를 사용한 GROUP BY 표현식의 결과
  - 열이 반영되지 않은 것은 NULL로 표현
  - 열 값에 NULL이 있어서 반환된 행과 사용자 입장에서 구분이 모호
- GROUPING 함수는 결과로 0 또는 1을 반환
- GROUPING 함수의 결과 해석 방식
  - 표현식을 사용하여 집계 값을 계산했으나 표현식 열에 있는 NULL 값이 열에 저장된 NULL 값이면 0을 반환
  - 표현식을 사용하지 않고 집계 값을 계산했으며 결과에 있는 NULL 값이 ROLLUP 또는 CUBE를 통한 그룹화의 결과이면 1을 반환
    <br>

> ♣︎ GROUPING SETS

- GROUPING SETS 연산자를 사용하여 하나의 쿼리에서 데이터를 여러 개로 그룹화하도록 지정

  - ROLLUP과 CUBE 연산자의 결과는 그룹화하는 열의 구분 값의 개수에 따라 결과가 너무 많이 변환되는 불편함이 존재
  - GROUPING SETS는 ROLLUP이나 CUBE에서 가능한 그룹화 가운데 실제 관심있는 그룹을 GROUP BY 절에 GROUPING SETS 다음에 지정
    <br>

- GROUPING SETS 연산자 사용 예시
  - GROUPING SETS((dept_id, position), (position, gender), ())
  - 결과 - GROUP BY dept_id, position - GROUP BY position, gender - GROUP BY 하지 않은 전체 사원의 수
    <br>

> ♣︎ 조합 열

- 그룹을 계산하는 동안 한 단위로 처리되는 둘 이상의 열의 모음

  - 조합 열은 ROLLUP, CUBE 및 GROUPING SETS에서 유용하게 사용
  - CUBE 또는 ROLLUP에서 조합 열을 사용하면 특정 레벨에 대해 집계를 건너뛰게 된다.
  - 조합열은 ROLLUP (a, (b, c), d) 과 같이 괄호 안에 열을 지정하여 사용
    <br>

- 조합 열 사용 예시
  - ROLLUP(dept_id, (gender, position))에는 다음의 결과가 함께 표시
    - GROUP BY (dept_id, gender, position)
    - GROUP BY(dept_id)
    - GROUP BY 하지 않은 결과
  - ➔ ROLLUP(dept_id, gender, position)의 결과에서 GROUP BY (dept_id, gender)의 결과 제외

```
SELECT dept_id, position, SUM(salary)
FROM y_emp
WHERE dept_id > 200
GROUP BY ROLLUP(dept_id, position);

SELECT dept_id, position, SUM(salary)
FROM y_emp
WHERE dept_id > 200
GROUP BY CUBE (dept_id, position);

SELECT dept_id, position, gender, COUNT(*)
FROM y_emp
GROUP BY GROUPING SETS ((dept_id, position), (position, gender), ());

SELECT dept_id, gender, position, SUM(salary)
FROM y_emp
GROUP BY ROLLUP(dept_id, (gender, position));
```
