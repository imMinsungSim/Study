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

<img width="420" height="260" alt="image" src="https://github.com/user-attachments/assets/4645cc1c-0101-4edd-bd35-e2cd3c19d29d" />   

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
