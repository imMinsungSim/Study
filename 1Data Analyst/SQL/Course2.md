Review

`집계 함수`

```
COUNT()    -- 개수
AVG()      -- 평균
SUM()      -- 합계
MAX()      -- 최댓값
MIN()      -- 최솟값
```

`집계 함수와 NULL`

집계 함수를 사용하는 컬럼에 있는 NULL이 있는 경우. NULL을 제외하고 계산 됨.

<img width="410" height="280" alt="image" src="https://github.com/user-attachments/assets/4645cc1c-0101-4edd-bd35-e2cd3c19d29d" />   

```
-- Q1. 아래 쿼리의 계산식을 적어보세요.
SELECT AVG(total_bill)
FROM tips
-> (16.99 + 10.34 + 21.01 + 23.68) / 4
-- Q2. 아래 쿼리의 계산식을 적어보세요.
SELECT SUM(total_bill) / COUNT(total_bill)
FROM tips
-> (16.99 + 10.34 + 21.01 + 23.68) / 4

-- Q3. 아래 쿼리의 계산식을 적어보세요.
SELECT SUM(total_bill) / COUNT(*)
-> (16.99 + 10.34 + 21.01 + 23.68) / 6
```

`GROUP BY` & `HAVING`

```
SELECT day          -- GROUP BY 기준이 되는 컬럼은 SELECT에도 반드시 적는다
     , SUM(total_bill) AS sales
FROM tips
WHERE sex = 'Female'
GROUP BY day
HAVING sales >= 200
ORDER BY sales DESC
LIMIT 1
```

`CASE`, `IF()`

```
SELECT CASE
            WHEN total_bill >= 40 THEN '큰 금액'
            WHEN total_bill >= 10 THEN '평균 금액'     -- 첫 번째 조건에서 걸러진 나머진 데이터
            ELSE '적은 금액'
          END AS sales_category
        , IF(day IN('Sat', 'Sun'), '주말', '평일') AS weekend
FROM tips
```

`조건문과 `GROUP BY` 함께 사용하기`

```
SELECT IF(day IN('Sat', 'Sun'), '주말', '평일') AS weekend
     , SUM(size) AS sum_size
FROM tips
GROUP BY weekend
```

`함수`

```
-- 날짜 더하기, 빼기
DATE_ADD()          -- 날짜 더하기
DATE_SUB()          -- 날짜 빼기
```
