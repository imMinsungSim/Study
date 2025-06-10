# SQL Basic 문법 연습

**데이터 가져오기(SELECT, FROM, LIMIT, DISTINCT)**

ex1) 테이블의 모든 칼럼을 다 출력해주세요. 데이터는 10개만 출력해주세요.

      SELECT * 
      FROM station 
      LIMIT 10 ; 

ex2) 테이블의 모든 컬럼을 가져오는 쿼리를 정류소 이름(name)과 주소(address)만 가져오는 쿼리로 수정해 봅시다.

      SELECT name
            ,address
      FROM station
      LIMIT 10;

ex3) station 테이블에서 소속 지자체(local)와 정류소 타입(type) 데이터를 가져오세요. 중복 데이터는 제외합니다.

      SELECT local
           ,type
      FROM station;

**조건에 맞는 데이터 검색하기(WHERE)**

ex1) ‘마포구'에 있는 따릉이 정류소만 뽑아주세요.

      SELECT *
      FROM station
      WHERE local = '마포구';

ex2) 위도(lat)가 37.6777보다 큰 정류소 중에 ‘도봉구’에 위치한 정류소 데이터만 뽑아주세요.

     SELECT *
     FROM station
     WHERE lat > 37.6777
       AND local = '도봉구';

ex3) ‘마포구’와 ‘광진구’에 있는 따릉이 정류소 데이터를 뽑아주세요(IN 활용).

      SELECT *
      FROM station
      WHERE local IN('마포구', '광진구');

ex4) 정류소 최근 갱신일(updated_at)이 2018년인 데이터를 뽑아주세요.

      SELECT *
      FROM station
      WHERE updated_at BETEWEEN '2018-01-01' AND '2018-12-31';

**패턴에 맞는 문자 찾기 (LIKE / NOT LIKE)**

ex1) 주소에 ‘망원동’이 들어가는 데이터를 뽑아주세요.

      SELECT *
      FROM station
      WHERE address LIKE '%망원동%';

ex2) 주소가 ‘서울특별시’로 시작하지 않는 데이터를 10개만 뽑아주세요.

      SELECT *
      FROM station
      WHERE address NOT LIKE '%서울특별시%';

**데이터 순서 정렬하기(ORDER BY)**

ex1) station 테이블을 station_id 기준으로 가장 큰 값부터 출력해 주세요.

      SELECT *
      FROM station
      ORDER BY station_id DESC;

ex2) ‘광진구’에 위치한 따릉이 정류소 중 최근 업데이트된(updated_at) 정류소부터 출력해 주세요. 만약 업데이트 된 날짜가 같다면, station_id가 작은 것부터 보여주세요.

      SELECT *
      FROM station
      ORDER BY updated at DESC, station_id;

**데이터 더하기, 빼기, 곱하기 (+,-,*)**

ex1)  tips 테이블 데이터 중에서 팁이 전체 식사 금액의 10%를 넘는 경우 데이터를 모두 출력해 주세요.
  
      SELECT *
      FROM tips
      WHERE tip > total_bill * 0.1

ex2) tips 테이블 데이터를 이용하여 tip 컬럼의 값을 2배로 출력하는 쿼리를 작성해 주세요. 결과 컬럼은 double_tip으로 출력해 주세요.

      SELECT tip * 2 as double_tip
      FROM tips
      
**데이터 나누기와 관련된 연산자 (/, DIV, %, MOD)**

ex1) 나누기 연산자(/)와 정수 나누기 연산자(DIV)를 이용하여 각 테이블에서 지불한 전체 식사 금액이 팁의 몇 배인지 계산하는 쿼리를 작성해 주세요.

      SELECT total_bill / tip
            ,total_bill DIV tip
      FROM tips
      
ex2) tips 테이블에서 size 컬럼이 짝수이면 0, 홀수이면 1을 출력하는 odd_even 컬럼을 출력해 주세요. size 컬럼도 함께 출력해 주세요.

      SELECT size
            ,size % 2 AS odd_even
      FROM tips

ex3) tips 테이블에서 size 컬럼이 짝수인 영수증만 출력해 주세요.

      SELECT *
      FROM tips
      WHERE size % 2 = 0

**데이터 개수 세기 (COUNT())**

ex1) tips 테이블에는 총 몇 개의 데이터가 들어있을까요?

      SELECT COUNT(*)
      FROM tips
      
ex2) 10불 이상 결제한 테이블은 몇 개 일까요?

      SELECT COUNT(*)
      FROM tips
      WHERE total_bill >= 10

ex3) 며칠 치 데이터가 들어있을까요?

      SELECT COUNT(DISTINCT day)
      FROM tips
      
**집계 함수 SUM(), AVG(), MIN(), MAX()**

ex1) 가게의 총매출액을 구해봅시다.

      SELECT SUM(total_bill)
      FROM tips 

ex2) 테이블당 평균 결제 금액을 구해봅시다.

      SELECT AVG(total_bill)
      FROM tips

ex3) 가장 결제 금액이 작았던 식사 금액과 컸던 식사 금액을 출력해 봅시다.

      SELECT MIN(total_bill)
            ,MAX(total_bill)
      FROM tips

**데이터 요약하기(GROUP BY, HAVING, ORDER BY)**

ex1) 요일별로 매출액의 합계를 구해봅시다.

      SELECT day
            ,SUM(total_bill)
      FROM tips
      GROUP BY day 

ex2) 요일, 시간대별로 매출액,팁의 합계를 구해봅시다.

      SELECT day
            ,time
            ,SUM(total_bill) as sales
            ,SUM(tip) as tips
      FROM tips
      GROUP BY day, time
      ORDER BY day ASC, time ASC

ex3) 요일별로 여성의 매출액 합계를 구해봅시다. 매출액 합계가 200불 미만인 날은 출력에서 제외하고, 매출액이 많은 날부터 출력하세요

      SELECT day
            ,SUM(total_bill) as sales
      FROM tips
      WHERE sex  'Female'
      GROUP BY day
      HAVING sales >= 200
      ORDER BY sales DESC

**[헷갈리는 부분 정리]** <br/>
언제 WHERE를 써야 하는지, 언제 HAVING을 써야 하는지 ? <br/>
아무런 가공을 하지 않은 원본 데이터에서 특정 조건을 만족하는 데이터를 뽑아올 때 사용하는 명령어가 WHERE이고요. <br/> 
HAVING은 GROUP BY를 사용하여 연산한 결과에서 특정 조건을 만족하는 데이터를 뽑아올 때 사용하는 명령어입니다. <br/>

      ```
      SELECT day
           , time
           , COUNT(*)
      FROM tips
      WHERE sex = 'Female'   -- 여성이 결제한 데이터만 뽑아 보겠다
      GROUP BY day, time     -- 요일 시간대별로 GROUP BY 해서 보겠다
      HAVING COUNT(*) >= 5   -- GROUP BY 후 데이터가 5개 이상인 그룹의 데이터만 보겠다
      ```

어

