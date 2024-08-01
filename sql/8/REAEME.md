
# 8. 실습 및 질의응답

## 실습 문제 제공
다양한 SQL 쿼리 작성 문제 제공

## 문제 풀이
실습 문제에 대한 풀이 및 설명

## Q&A 세션
학생들의 질문에 대한 답변 및 추가 설명




# SQL 실습 문제 및 풀이

## 1. 기본 쿼리
### 문제 1: SELECT 문 사용하기
**문제:**
```sql
-- 테이블 employees에서 모든 열을 선택하세요.
SELECT * FROM employees;
```

### 문제 2: WHERE 절 사용하기
**문제:**
```sql
-- employees 테이블에서 부서가 'Sales'인 직원들의 이름과 부서를 선택하세요.
SELECT name, department FROM employees WHERE department = 'Sales';
```

### 문제 3: ORDER BY 사용하기
**문제:**
```sql
-- employees 테이블에서 직원들의 이름을 알파벳 순으로 정렬하세요.
SELECT name FROM employees ORDER BY name;
```

### 문제 4: DISTINCT 사용하기
**문제:**
```sql
-- employees 테이블에서 중복을 제거한 부서 목록을 선택하세요.
SELECT DISTINCT department FROM employees;
```

### 문제 5: LIMIT 사용하기
**문제:**
```sql
-- employees 테이블에서 상위 5명의 직원 정보를 선택하세요.
SELECT * FROM employees LIMIT 5;
```

## 2. 조인 (JOIN)
### 문제 6: INNER JOIN 사용하기
**문제:**
```sql
-- employees 테이블과 departments 테이블을 조인하여 직원의 이름과 부서명을 선택하세요.
SELECT e.name, d.department_name 
FROM employees e 
INNER JOIN departments d ON e.department_id = d.department_id;
```

### 문제 7: LEFT JOIN 사용하기
**문제:**
```sql
-- employees 테이블과 departments 테이블을 조인하여 모든 직원의 이름과 해당하는 부서명을 선택하세요. 부서가 없는 직원도 포함하세요.
SELECT e.name, d.department_name 
FROM employees e 
LEFT JOIN departments d ON e.department_id = d.department_id;
```

### 문제 8: RIGHT JOIN 사용하기
**문제:**
```sql
-- employees 테이블과 departments 테이블을 조인하여 모든 부서와 해당 부서에 소속된 직원의 이름을 선택하세요. 직원이 없는 부서도 포함하세요.
SELECT e.name, d.department_name 
FROM employees e 
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

### 문제 9: FULL OUTER JOIN 사용하기
**문제:**
```sql
-- employees 테이블과 departments 테이블을 조인하여 모든 직원과 부서를 선택하세요.
SELECT e.name, d.department_name 
FROM employees e 
FULL OUTER JOIN departments d ON e.department_id = d.department_id;
```

### 문제 10: CROSS JOIN 사용하기
**문제:**
```sql
-- employees 테이블과 departments 테이블을 크로스 조인하여 가능한 모든 직원과 부서 조합을 선택하세요.
SELECT e.name, d.department_name 
FROM employees e 
CROSS JOIN departments d;
```

## 3. 서브쿼리 (Subquery)
### 문제 11: WHERE 절에서 서브쿼리 사용하기
**문제:**
```sql
-- 부서명이 'Sales'인 직원들의 이름을 선택하세요.
SELECT name 
FROM employees 
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
```

### 문제 12: SELECT 절에서 서브쿼리 사용하기
**문제:**
```sql
-- 직원들의 이름과 그들의 부서명을 선택하세요.
SELECT name, 
       (SELECT department_name FROM departments WHERE department_id = employees.department_id) AS department_name 
FROM employees;
```

### 문제 13: FROM 절에서 서브쿼리 사용하기
**문제:**
```sql
-- 부서별 직원 수를 선택하세요.
SELECT d.department_name, COUNT(e.employee_id) AS employee_count 
FROM departments d 
JOIN (SELECT department_id, employee_id FROM employees) e 
ON d.department_id = e.department_id 
GROUP BY d.department_name;
```

## 4. 그룹화 및 집계 함수
### 문제 14: GROUP BY 사용하기
**문제:**
```sql
-- 부서별 평균 급여를 선택하세요.
SELECT department_id, AVG(salary) AS average_salary 
FROM employees 
GROUP BY department_id;
```

### 문제 15: HAVING 절 사용하기
**문제:**
```sql
-- 평균 급여가 50000 이상인 부서들을 선택하세요.
SELECT department_id, AVG(salary) AS average_salary 
FROM employees 
GROUP BY department_id 
HAVING AVG(salary) >= 50000;
```

## 5. 고급 SQL
### 문제 16: 윈도우 함수 사용하기
**문제:**
```sql
-- 각 직원의 급여와 동일 부서 내에서의 급여 순위를 선택하세요.
SELECT name, salary, 
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank 
FROM employees;
```

### 문제 17: 공통 테이블 표현식 (CTE) 사용하기
**문제:**
```sql
-- 직원들의 이름과 매니저 이름을 선택하세요.
WITH ManagerCTE AS (
    SELECT e1.employee_id, e1.name AS employee_name, e2.name AS manager_name 
    FROM employees e1 
    LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id
)
SELECT * FROM ManagerCTE;
```

### 문제 18: 트랜잭션 사용하기
**문제:**
```sql
-- 트랜잭션을 사용하여 직원의 급여를 업데이트하고 변경 내용을 커밋하세요.
START TRANSACTION;

UPDATE employees 
SET salary = salary * 1.1 
WHERE department_id = 1;

COMMIT;
```

### 문제 19: 인덱스 사용하기
**문제:**
```sql
-- employees 테이블의 department_id 열에 인덱스를 생성하세요.
CREATE INDEX idx_department_id ON employees(department_id);
```

## 6. 실습 테이블 생성
```sql
-- employees 테이블 생성
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    salary DECIMAL(10, 2),
    manager_id INT
);

-- departments 테이블 생성
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

-- 예제 데이터 삽입
INSERT INTO employees (employee_id, name, department_id, salary, manager_id)
VALUES (1, 'John Doe', 1, 50000, NULL),
       (2, 'Jane Smith', 2, 60000, 1),
       (3, 'Jim Brown', 1, 55000, 1),
       (4, 'Jake White', 3, 70000, NULL),
       (5, 'Jill Black', 2, 65000, 1);

INSERT INTO departments (department_id, department_name)
VALUES (1, 'Sales'),
       (2, 'Marketing'),
       (3, 'Engineering');
```

