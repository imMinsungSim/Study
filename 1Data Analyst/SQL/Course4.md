## REVIEW

`Outer Join(LEFT JOIN, RIGHT JOIN)`

```
SELECT grades
     , COUNT(c.id) customers
FROM customers c
     LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL
GROUP BY grades
```

`Self Join`

```
SELECT *
FROM employees e
     INNER JOIN employees m ON e.manager_id = m.employee_id
WHERE m.employee_id IS NOT NULL
ORDER BY e.employee_id
```

#### AARRR
- A(Acquisition, 획득) : 광고 등의 방법으로 새로운 사용자를 얻어오는 단계
- A(Activation, 활성화) : 회원 가입, 듀토리얼 등 사용자를 활성화 시키는 단계 
- R(Retention, 리텐션) : 지속적으로 서비스를 사용하게 만드는 단계
- R(Revenue, 매출) : 매출을 만드는 단계
- R(Feferral, 추천) : 다른 사용자에게 제품을 추천하는 단계

<br>

#### 매출에 영향을 주는 요소
- 활성 사용자 수
- 구매 고객 수(PU, Paying User)
- 고객 1인당 평균 구매액
  - ARPU(Average Revenue Per User) : 전체 매출 / 활성 사용자 수
  - ARPPU(Average Revenue Per Paying User) : 전체 매출 / 구매 고객 수

`일별 매출액, PU, ARPPU`

```
SELECT o.order_date
     , ROUND(SUM(oi.price * oi.quantity), 2) AS revenue_daily
     , COUNT(DISTINCT o.customer_id) AS pu
     , ROUND(SUM(oi.price * oi.quantity), 2) / COUNT(DISTINCT o.customer_id) AS arppu
FROM order_itmes oi
     INNER JOIN order o ON o.order_id = oi.order_id
WHERE o.order_id NOT LIKE 'C%'
GROUP BY o.order_date
ORDER BY o.order_date
```


