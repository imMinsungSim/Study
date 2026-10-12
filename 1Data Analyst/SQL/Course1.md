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

'As'
```
SELECT address AS station_address       -- 별칭 붙이기
FROM station
```

'조건에 맞는 데이터 검색하기'
SELECT *
FROM station
WHERE lat > 37.6777                      -- 비교 연산자
  OR local IN ('마포구', 광진구')          -- 여러개의 데이터 한꺼번에 찾기
  OR updated_at BETWEEN '2018-01-01 00:00:00' AND '2018-12-31 23:59:59'
  OR type IS NULL                         -- 값이 없는 데이터 찾기
  OR type IS NOT NULL                     
  OR local LIKE '강남_'                    -- 패턴에 맞는 문자 찾기
  OR address NOT LIKE '서울특별시%'
LIMIT 50

'함수'
-- 문자열 자르고 붙이기
LEFT()          -- 왼쪽에 있는 문자열 가져오기
RIGHT()         -- 오른쪽에 있는 문자열 가져오기
SUBSTRING()     -- 문자열 자르기, SUBSTR()로 사용하기도 함
CONCAT()        -- 문자열 붙이기

-- 소수점 처리
ROUND()          -- 소수점 반올림
CEILING()        -- 소수점 올림, CEIL()로 사용하기도 함
FLOOR()          -- 소수점 내림
FORMAT()         -- 숫자를 반올림 하고 '#,###,###.##' 형태로 변환
