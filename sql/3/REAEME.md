
# 3. 기본 쿼리 작성

## SELECT 사용 예시
데이터베이스에서 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블명;
```

## 조건문 (WHERE)
특정 조건을 만족하는 데이터를 조회하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블명
WHERE 조건;
```

## 정렬 (ORDER BY)
데이터를 특정 열을 기준으로 정렬하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블명
ORDER BY 열1 ASC|DESC;
```

## 중복 제거 (DISTINCT)
중복된 데이터를 제거하고 조회하는 데 사용
```
SELECT DISTINCT 열1
FROM 테이블명;
```

## 제한 (LIMIT)
조회할 데이터의 개수를 제한하는 데 사용
```
SELECT 열1, 열2, ...
FROM 테이블명
LIMIT 숫자;
```
