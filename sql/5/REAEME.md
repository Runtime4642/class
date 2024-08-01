
# 5. 서브쿼리 (Subquery)

## 서브쿼리 개념 및 예제
다른 쿼리 내에 포함된 쿼리
```
SELECT 열1, 열2, ...
FROM 테이블명
WHERE 열3 IN (SELECT 열3 FROM 다른_테이블명 WHERE 조건);
```

## WHERE 절에서의 서브쿼리
```
SELECT 열1, 열2, ...
FROM 테이블명
WHERE 열3 = (SELECT 열3 FROM 다른_테이블명 WHERE 조건);
```

## SELECT 절에서의 서브쿼리
```
SELECT 열1, 열2, (SELECT 열3 FROM 다른_테이블명 WHERE 조건) AS 열명
FROM 테이블명;
```

## FROM 절에서의 서브쿼리
```
SELECT 열1, 열2
FROM (SELECT 열1, 열2 FROM 다른_테이블명 WHERE 조건) AS 서브쿼리_별칭;
```
