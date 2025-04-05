~~SQL 쿼리를 작성하다가 만나는 다양한 오류~~


~~4-1. INTRO~~
# 4-2 데이터 타입과 변환을 위한 함수(CAST, SAFE_CAST)

- SELECT 문에서 데이터를 변환시킬 수 있음 
-또는 WHERE의 조건문에서도 사용할 수 있음   

- 데이터 타입 : 숫자, 문자, 시간, 날짜, 부울(Bool), JSON, ARRAY 등 다양

- 보이는 것과 저장된 것의 차이가 존재 ( 데이터 타입이 중요한 이유 )   

- 자료 타입 변경하기 : CAST  *ex) SELECT CAST(1 AS STRING) # 숫자 1을 문자 1로 변경*  

- 더 안전하게 데이터 타입 변경하기 : SAFE_CAST (변환이 실패할 경우 NULL 반환)
- 수학 함수도 존재 
  *TIP) 나누기를 할 경우 x/y 대신 SAFE_DIVIDE 함수 사용 ( x, y 중 하나라도 0인 경우 그냥 나누면 zero error가 발생)*  

# 4-3 문자열 함수 


![](/image_SQL/4-1.png)
![](/image_SQL/4-2.png)  
![](/image_SQL/4-3.png)  
![](/image_SQL/4-4.png)  
![](/image_SQL/4-5.png)  
![](/image_SQL/4-6.png)




# 4-4 날짜 및 시간 데이터 이해하기 (1) 
~~~
 유저가 어떤 행위를 했을 때 항상 시간이 붙고 시간의 흐름에 따라 데이터를 분석함  ex) created at, updated at
~~~
1) 날짜 및 시간 데이터 타입 파악 : DATE, DATETIME, TIMESTAMP  
- DATE : DATE만 표시하는 데이터 ex) 2023-12-31  
- DATETIME : DATE와 TIME까지 표시하는 데이터, Time Zone 정보 없음, ex) 2023-12-31 14:00:00    
- TIME : 날짜와 무관하게 시간만 표시하는 데이터 ex) 23:59:59.00 
2) 날짜 및 시간 데이터 관련 알면 좋은 내용 : UTC, Millisecond  
- **타임존(누락됐는지 확인!!)**  
- UTC(한국시간 : UTC+9) : 국제적인 표준 시간, 타임존( 특정 지역의 표준 시간대)이 존재  
- TIMESTAMP : 1970년 1월 1일 00:00:00 (UTC) 로부터 경과한 시간을 나타낸 값 ex) 2023-12-31 14:00:00 UTC   
- millisecond(ms) : 천 분의 1초(1,000ms = 1초), 빠른 반응이 필요한 분야에서 사용(초보다 더 정확하게)
- microsecond(μs) : 1/1,000ms, 1/1,000,000초  


3) 날짜 및 시간 데이터 타입 변환 

![](/image_SQL/4-7.png)
![](/image_SQL/4-8.png)

4) 시간 함수(두 시간의 차이, 특정 부분 추출하기)

회사의 데이터들은 대부분 시간과 관련된 데이터가 존재  & TIMESTAMP <=> DATETIME 변환  


![](/image_SQL/4-9.png)

![](/image_SQL/4-10.png)


 
