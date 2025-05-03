## 4-4.날짜 및 시간 데이터 이해하기(2) 

DATETIME 함수 - CURRENT_DATETIME

CURRENT_DATETIME(Ptime_zone]) : 현재 DATETIME 출력  


5-1

EXTRACT : DATETIME에사 특정 부분만 추출하고 싶은 경우  

예시) 일자별 주문, 월별 주문을 따로 뽑고 싶을 때 

**강의대로 하면 오류 발생(약간 수정)**  


- EXTRACT 함수에서는 DATE 자체를 추출할 수 없음
- `EXTRACT(DATE FROM ...)`는 문법 오류이며 DATE는 추출 가능한 요소가 아니라 자료형이기 때문임
- 전체 날짜가 필요하면 `DATE(DATETIME(...))`을 사용해야 함
- 요약:
  - `EXTRACT()`는 날짜의 구성 요소 추출용
  - `DATE()`는 DATETIME이나 TIMESTAMP에서 전체 날짜 추출용

EXTRACT(part FROM datetime_expression)

예시) 

5-2

### 요일을 추출하고 싶은 경우 
EXTRACT(DAYOFWEEK FROM date_time_col) 
- 한주의 첫날이 일요일인 [1,7] 범위의 값을 반환  

5-3 


