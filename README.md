# Study

SQL

데이터 가져오기(SELECT, FROM, LIMIT, DISTINCT)

ex1) 테이블의 모든 칼럼을 다 출력해주세요. 데이터는 10개만 출력해주세요.
      SELECT * 
      FROM station 
      LIMIT 10

ex2) 테이블의 모든 컬럼을 가져오는 쿼리를 정류소 이름(name)과 주소(address)만 가져오는 쿼리로 수정해 봅시다.
      SELECT name
            ,address
      FROM station
      LIMIT 10

ex3) station 테이블에서 소속 지자체(local)와 정류소 타입(type) 데이터를 가져오세요. 중복 데이터는 제외합니다.
      SELECT local
           ,type
      FROM station

조건에 맞는 데이터 검색하기(WHERE)

ex1) ‘마포구'에 있는 따릉이 정류소만 뽑아주세요.
      SELECT *
      FROM station
      WHERE local = '마포구'

ex2) 위도(lat)가 37.6777보다 큰 정류소 중에 ‘도봉구’에 위치한 정류소 데이터만 뽑아주세요.
     SELECT *
     FROM station
     WHERE lat > 37.6777
       AND local = '도봉구'

ex3) ‘마포구’와 ‘광진구’에 있는 따릉이 정류소 데이터를 뽑아주세요(IN 활용).
      SELECT *
      FROM station
      WHERE local IN('마포구', '광진구')
  
