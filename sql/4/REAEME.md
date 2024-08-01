
# 4. 조인 (JOIN)

## INNER JOIN
두 테이블에서 매칭되는 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블1
INNER JOIN 테이블2 ON 테이블1.열 = 테이블2.열;
```

## LEFT JOIN
왼쪽 테이블의 모든 데이터와 매칭되는 오른쪽 테이블의 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블1
LEFT JOIN 테이블2 ON 테이블1.열 = 테이블2.열;
```

## RIGHT JOIN
오른쪽 테이블의 모든 데이터와 매칭되는 왼쪽 테이블의 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블1
RIGHT JOIN 테이블2 ON 테이블1.열 = 테이블2.열;
```

## FULL OUTER JOIN
두 테이블에서 매칭되는 모든 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블1
FULL OUTER JOIN 테이블2 ON 테이블1.열 = 테이블2.열;
```

## CROSS JOIN
두 테이블의 모든 가능한 조합을 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블1
CROSS JOIN 테이블2;
```
