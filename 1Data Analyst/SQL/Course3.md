## REVIEW

#### RFM(Recency, Frequency, Monetary) 고객 세분화 분석
- Recency : 얼마나 최근에 구매했는지
- Frequency : 얼마나 자주 구매했는지
- Monetary : 얼마나 많은 금액을 구매했는지

```
SELECT CASE WHEN last_order_date >= '2020-12-01' THEN 'recent' ELSE 'past' END recency
     , CASE WHEN cnt_orders >= 3 THEN 'high' ELSE 'low' END frequency
     , CASE WHEN sum_sales >= 500 THEN 'high' ELSE 'low' END monetary
     , COUNT(DISTINCT customer_id) customers
FROM customer_stats
GROUP BY recency, frequency, monetary
ORDER BY recency DESC
```

`테이블 피봇`

```
SELECT region AS Region
     , COUNT(CASE WHEN category = 'Furniture' THEN order_id END) AS Furniture
FROM records
GROUP BY region
```

`UNION`, `UNION ALL`

```
SELECT *
FROM customers_before_2021

UNION ALL

SELECT *
FROM customers_after_2021
```

`INNER JOIN`

```
SELECT *
FROM orders AS o
     INNER JOIN customers AS c ON o.customer_id = c.customer_id
WHERE c.country = 'France'
```
