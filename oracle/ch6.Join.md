## 조인
---

> ♣︎ 조인의 개념과 종류
- 하나의 SELECT 문 안에서 여러 테이블로부터의 데이터를 사용하는 것
<p align ="center"><img src="./img/Join/조인의%20개념.png" height="400px"></img></p>
<br>

> ♣︎ 정규화(검증단계)
- 관계형 데이터베이스는 중복을 최소화하고 갱신 작업의 이상현상을 제거하기위하여 설계 시 수행하는 과정
- 정규화의 결과 테이블에는 필요한 최소한의 정보를 저장하게 되어 보고서를 생성하려면 여러 테이블의 데이터를 사용해야 하는 경우 발생 => 조인 필요
<br>

> ♣︎ 조인의 종류
- 조인되는 두 테이블의 연관되는 데이터의 비교 방식
  - 등가조인(Equi Join) : 같은 자료가 있는 테이블 끼리 조인
  - 비등가조인(Non Equi Join) : 같은 자료가 없어도 테이블 끼리 조인
- 조인의 결과에 따른 분류
  - Inner Join
  - Outer Join
- 조인에 사용되는 테이블 수에 의한 분류
  - Self Join : 테이블 한개로 조인
  - 3 Way Join : 3개의 테이블로 조인

### ANSI/ISO SQL 표준 조인
---

> ♣︎ SQL: 1999 표준 조인 구문
- FROM 절의 두 테이블 이름 사이에 JOIN 방식과 함께 JOIN 절 입력
  - Cross Join
  - Natural Join
  - USING 절을 사용하는 JOIN 구문
  - ON 절을 사용하는 JOIN rnans
  - LEFT / RIGHT / FULL OUTER JOIN

> ♣︎ CROSS JOIN (모든 경우의 수를 조인 해봄)
- 두 테이블 간의 Cartesian Product과 동일한 결과
- 두 테이블간의 상호 가능한 모든 조합을 결과로 반환
- FROM절의 두 테이블 사이에 CROSS JOIN 키워드를 지정
- 구문
```
SELECT [table1.]column, [table2.]column 
FROM table1 CROSS JOIN table2;
```
- 두 테이블의 행수를 곱한 수를 결과로 반환
<br>

> ♣︎ NATURAL JOIN (조인을 가능한 조인이 하나일때 사용)
- JOIN 하는 두 테이블에 열 이름과 데이터 유형이 동일한 열을 각각 포함하고 있다면 그 열을 기준으로 자동으로 조인을 수행
  - 두 테이블 모두에서 이름과 데이터 유형이 동일한 열에서만 가능
  - 열의 이름은 같지만 데이터 유형이 다를 경우 NATURAL JOIN 구문에서 오류가 발생
- 구문
```
SELECT [table1.]column, [table2.]column 
FROM table1 NATURAL JOIN table2;
```

```
SELECT emp_name, dept_name
FROM y_emp CROSS JOIN y_dept; // y_emp와 y_dept간의 상호 가능한 모든 조합을 결과로 출력

SELECT dept_id, dept_name, city
FROM y_dept NATURAL JOIN y_loc
WHERE dept_id IN(100, 200);
```
<br>

> ♣︎ USING 절을 사용하는 JOIN 문의 작성(컬럼 이름이 같으면 사용)
- 둘 이상의 열이 일치하는 테이블 간의 조인에서 사용할 열을 명시적으로 지정
- 열 이름이 같지만 유형이 다른 경우에도 오류 없이 조인을 수행
- 구문

```
SELECT [table1.]column, [table2.]column 
FROM table1 JOIN table2
USING (column);
```
<br>

> ♣︎ 테이블의 접두어의 사용
- 조인되는 두 테이블에 동일한 이름의 열이 존재하는 경우
  - 열 이름 앞에 테이블 이름을 지정하여 열을 검색할 테이블을 한정
  - 테이블 접두어를 사용하지 않으면 조인되는 두 테이블에 모두 포함돈 열의 경우 오류를 반환
  - ex) 다음과 같이 y_emp 테이블과 y_dept 테이블을 dept_id열을 기준으로 조인하면서 mgr_id열이 선택된 경우 오류 반환
```
SELECT emp_id, emp_name, mgr_id, dept_id, dept_name FROM y_emp JOIN y_dept
USING (dept_id);
SELECT emp_id, emp_name, mgr_id, dept_id, dept_name
                 * 
ERROR at line 1:
ORA-00918: column ambiguously defined
```
<br>

> ♣︎ 테이블 별칭의 사용
- 열 이름을 한정하기위해 테이블 접두어 대신 테이블 alias 사용
  - 긴 이름의 테이블에 적합
  - SQL 코드를 더 작게 유지
- 테이블 alias 사용 방법
  - 테이블 이름 뒤에 공백이 온 후에 테이블 alias 지정
  - SELECT 문에서 테이블 이름을 대신하므로 의미있는 이름으로 지정
  - 최대 30자까지 가능하지만 짧을수록 좋음

```
SELECT emp_id, emp_name, dept_id, dept_name
FROM y_emp JOIN y_dept
USING(dept_id);

SELECT y_emp.emp_name, y_emp.mgr_id, dept_id, y_dept.dept_name
FROM y_emp JOIN y_dept
USING (dept_id);

SELECT e.emp_id, e.emp_name, dept_id, d.dept_name
FROM y_emp e JOIN y_dept d
USING(dept_id);

SELECT y_emp.emp_id, e.emp_name, dept_id, d.dept_name
FROM y_emp e JOIN y_dept d
USING(dept_id); // 별칭을 사용한 경우 명령문에 테이블 이름을 사용하면 오류
```
<br>

> ♣︎ EQUI JOIN과 NON EQUI JOIN
- Equi Join 이란?
  - 단순 조인 또는 내부 조인(inner join)
  - 두 테이블에서 연관이 있는 데이터에 대하여 동등비교를 수행
  - 일반적으로 가장 많이 사용되는 조인방식
  - 주로 기본키와 외래키 관계에 있는 두 테이블 간에 자주 사용
  - NATURAL JOIN 이나 USING절을 사용하는 조인은 Equi Join만 가능
- Non Equi Join 이란?
  - 조인 조건에 동등연산자(등호,=)가 아닌 연산자를 사용하여 두 테이블의 관계를 기술하는 조인
<br>

> ♣︎ ON 절을 사용하는 등가조인
- ON 절 사용 시 열의 이름이 다른 두 테이블 간의 Equi Join도 가능
  - 여러 가지 조인조건을 ON절에 직접 지정
  - WHERE 절의 다른 검색조건과 조인조건 분리
  - 사용자 입장에서 코드를 이해하기 용이함
- 구문
```
SELECT [table1.]column, [table2.]column 
FROM table1 JOIN table2
ON (table1.column = table2.column);
```

```
SELECT d.dept_id, d.dept_name, d.loc_id, l.city
FROM y_dept d JOIN y_loc l
ON(d.loc_id = l.loc_id);

SELECT e.emp_id, e.emp_name, e.dept_id, d.dept_name
FROM y_emp e JOIN y_dept d
ON(e.dept_id = d.dept_id)
WHERE e.salary > 650;
```
<br>

> ♣︎ ON 절을 사용하는 여러가지 조인
- 비등가조인(NON EQUI JOIN)
  - ON절에는 임의의 연산자 사용이 가능하므로 비등가 조인도 가능
  - 주로 BETWEEN 연산자가 많이 사용
- 자체조인(SELF JOIN)
  - 하나의 테이블을 두 번 검색해서 조인
  - FROM 절에 지정한 테이블 두 개가 실제 동일한 테이블
- 3 Way 조인
  - 세 개의 테이블을 조인하는 것을 의미
  - 세 개의 테이블을 조인하여 더 많은 테이블을 조합하여 다양한 결과를 생성
```
SELECT e.emp_id, e.emp_name, e.salary, p.pay_level 
FROM y_emp e JOIN pay_grade p
ON e.salary BETWEEN p.low_pay AND p.high_pay ;

SELECT e.emp_id, e.emp_name, e.mgr_id, m.emp_name 
FROM y_emp e JOIN y_emp m
ON (e.mgr_id = m.emp_id);

SELECT emp_name, dept_name, city 
FROM y_emp JOIN y_dept
ON (y_emp.dept_id = y_dept.dept_id) 
JOIN y_loc
ON (y_dept.loc_id = y_loc.loc_id);
```
<br>

> ♣︎ INNER JOIN과 OUTER JOIN의 개념
- INNER JOIN(내부조인)
  - 조인하는 열에 대해 양쪽 테이블 모두에서 일치하는 행만 반환
  - 조인 조건에 만족하는 값을 갖지 못한 행은 결과에서 누락
  - 예 : 전체 사원은 33명인데 y_emp 테이블과 y_dept 테이블을 조인하면 부서가 NULL인 사원은 결과에서 제외되어 32명의 사원만 결과로 반환
- OUTER JOIN(외부조인)
  - INNER JOIN의 결과와 함께 INNER JOIN 시 누락된 행을 함께 표시
  - 예 : y_emp 테이블과 y_dept 테이블을 OUTER JOIN 시 부서가 NULL인 사원 또는 사원이 배치되지 않아서 누락된 부서정보를 INNER JOIN의 결과와 함께 반환
<br>

> ♣︎ OUTER JOIN
- LEFT OUTER JOIN
  - INNER JOIN의 결과와 함께 JOIN 구문을 기준으로 일치하는 행이 없는 왼쪽테이블의 행을 반환하는 조인
- RIGHT OUTER JOIN
  - 동일한 방식으로 일치하는 행이 없는 오른쪽테이블의 행을 반환하는 조인
- FULL OUTER JOIN
  - 두 가지 결과를 함께 반환하는 조인
<br>

- OUTER JOIN의 구문
  - FROM 절에 LEFT/RIGHT/FULL OUTER JOIN을 명시하고 ON 절에는 조인조건만 지정
- 구문
```
SELECT [table1.]column, [table2.]column
FROM table1 [LEFT | RIGHT | FULL] OUTER JOIN table2 
ON (table1.column = table2.column);
```
```
SELECT e.emp_name, e.dept_id, d.dept_name 
FROM y_emp e LEFT OUTER JOIN y_dept d 
ON (e.dept_id = d.dept_id);

SELECT e.emp_name, d.dept_id, d.dept_name 
FROM y_emp e RIGHT OUTER JOIN y_dept d 
ON (e.dept_id = d.dept_id) ;

SELECT e.emp_name, e.dept_id, d.dept_name 
FROM y_emp e FULL OUTER JOIN y_dept d 
ON (e.dept_id = d.dept_id) ;
```

### 오라클 전용 조인(비표준)
> ♣︎ 오라클 전용 조인 구문
- Oracle 8i 릴리스까지 오라클 조인의 유일한 방식
  - 이전에 개발된 응용프로그램에는 오라클 전용조인을 포함
- 구문
```
SELECT table1.column, table2.column 
FROM table1, table2
WHERE table1.column1 = table2.column2;
```
<br>

> ♣︎ 오라클 전용 조인
- 오라클 조인의 종류
  - Equi Join
  - Non-Equi Join
  - Outer Join
  - self Join
  - Cartesian Product
<br>

> ♣︎ 오라클 조인 구문 작성의 유의사항
- WHERE 절에 조인 조건을 작성
- 다른 조건을 AND연산자를 사용하여 추가
- n개의 테이블을 조인 시 최소 n-1개의 조인 조건이 필요
  - 예를들어 네 개의 테이블을 조인하려면 최소 세 개의 조인 조건이 필요
- 아우터조인 시 아우터조인 연산자(+) 사용
  - 정보가 누락된 테이블 방향에 아우터조인 연산자(+) 추가
```
SELECT e.emp_id, e.emp_name, e.dept_id, d.loc_id 
FROM y_emp e, y_dept d
WHERE e.dept_id = d.dept_id
AND e.dept_id BETWEEN 100 AND 300;

SELECT e.emp_id, e.emp_name, e.salary, p.pay_level 
FROM y_emp e, pay_grade p
WHERE e.salary BETWEEN p.low_pay AND p.high_pay;

SELECT e.emp_name, d.dept_name, l.city 
FROM y_emp e, y_dept d, y_loc l 
WHERE e.dept_id = d.dept_id
AND d.loc_id = l.loc_id;

SELECT e.emp_id, e.emp_name, e.mgr_id, m.emp_name 
FROM y_emp e, y_emp m
WHERE e.mgr_id = m.emp_id;

ELECT e.emp_id, e.emp_name, e.dept_id, d.dept_name 
FROM y_emp e, y_dept d
WHERE e.dept_id=d.dept_id(+);

SELECT e.emp_id, e.emp_name, e.dept_id, d.dept_name 
FROM y_emp e, y_dept d
WHERE e.dept_id(+) = d.dept_id ;
```
