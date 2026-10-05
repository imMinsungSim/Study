#### Review

`SELECT`, `FROM`, `ORDER BY`, `LIMIT`

```
SELECT name
     , adderss                                   -- 특정 열 선택하기
FROM station                                     -- 테이블 이름
ORDER BY updated_at DESC, station_id ASC         -- 2개 이상 컬럼으로 정렬하기
LIMIT 5
```

`DISTINCT`

```
SELECT DISTINCT name     -- 중복 제거하기
FROM station
```



