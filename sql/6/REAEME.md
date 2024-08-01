
# 6. 그룹화 및 집계 함수

## GROUP BY 사용법
데이터를 그룹화하여 집계하는 데 사용
```
SELECT 열1, COUNT(*)
FROM 테이블명
GROUP BY 열1;
```

## 집계 함수
### COUNT
```
SELECT COUNT(열)
FROM 테이블명
WHERE 조건;
```

### SUM
```
SELECT SUM(열)
FROM 테이블명
WHERE 조건;
```

### AVG
```
SELECT AVG(열)
FROM 테이블명
WHERE 조건;
```

### MAX
```
SELECT MAX(열)
FROM 테이블명
WHERE 조건;
```

### MIN
```
SELECT MIN(열)
FROM 테이블명
WHERE 조건;
```

## HAVING 절
GROUP BY로 그룹화된 데이터에 조건을 적용하는 데 사용
```
SELECT 열1, COUNT(*)
FROM 테이블명
GROUP BY 열1
HAVING COUNT(*) > 숫자;
```
