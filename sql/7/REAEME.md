
# 7. 고급 SQL

## 윈도우 함수
특정 윈도우(행 그룹) 내에서 데이터의 집계를 수행
```
SELECT 열1, 열2, SUM(열3) OVER (PARTITION BY 열1 ORDER BY 열2) AS 윈도우_합계
FROM 테이블명;
```

## 공통 테이블 표현식 (CTE)
쿼리의 재사용과 가독성을 높이는 데 사용
```
WITH CTE명 AS (
  SELECT 열1, 열2
  FROM 테이블명
  WHERE 조건
)
SELECT 열1, 열2
FROM CTE명
WHERE 조건;
```

## 트랜잭션 (Transactions)
일련의 SQL 작업들을 하나의 단위로 묶어 처리
```
BEGIN;
UPDATE 테이블명 SET 열1 = 값1 WHERE 조건;
INSERT INTO 테이블명 (열1, 열
2) VALUES (값1, 값2);
COMMIT;
```

## 인덱스 (Indexes)
데이터베이스 검색 속도를 높이는 데 사용
```
CREATE INDEX 인덱스명
ON 테이블명 (열1);
```