## 4-4.날짜 및 시간 데이터 이해하기(2) 

DATETIME 함수 - CURRENT_DATETIME

CURRENT_DATETIME(Ptime_zone) : 현재 DATETIME 출력  



![](/image_SQL/5-1.PNG)  


EXTRACT : DATETIME에서 특정 부분만 추출하고 싶은 경우  

예시) 일자별 주문, 월별 주문을 따로 뽑고 싶을 때 

**강의대로 하면 오류 발생(약간 수정)**  


- EXTRACT 함수에서는 DATE 자체를 추출할 수 없음
- `EXTRACT(DATE FROM ...)`는 문법 오류이며 DATE는 추출 가능한 요소가 아니라 자료형이기 때문임
- 전체 날짜가 필요하면 `DATE(DATETIME(...))`을 사용해야 함
- 요약:
  - `EXTRACT()`는 날짜의 구성 요소 추출용
  - `DATE()`는 DATETIME이나 TIMESTAMP에서 전체 날짜 추출용

EXTRACT(part FROM datetime_expression)


### 요일을 추출하고 싶은 경우 
EXTRACT(DAYOFWEEK FROM date_time_col) 
- 한주의 첫날이 일요일인 [1,7] 범위의 값을 반환  


![](/image_SQL/5-3.PNG)  


### DATETIME 함수 - DATETIME_TRUNC

DATE와 HOUR만 남기고 싶은 경우 => **시간 자르기** 

![](/image_SQL/5-4.PNG)  


## PARSE_DATETIME  

문자열로 저장된 DATETIME을 DATETIME 타입으로 바꾸고 싶은 경우  

![](/image_SQL/5-5.PNG)  


## FORMAT_DATETIME  


DATETIME 타입 데이터를 특정 형태의 **문자열** 데이터로 변환하고 싶은 경우  



![](/image_SQL/5-6.PNG)  


## LAST_DAY  

마지막 날을 알고 싶은 경우 : 자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우  


![](/image_SQL/5-7.PNG)  


- MONTH가 디폴트
-  WEEK : WEEK기준으로 마지막 날짜, 디폴트는 일요일기준 
- WEEK(MONDAY) : 월요일을 기준으로 마지막날 => 일요일 
- 보통 LAST_DAY는 MONTH기준(디폴트)으로 많이 활용 

## DATETIME_DIFF  

두 DATETIME의 차이를 알고 싶은 경우  


## 시간 데이터 연습 문제  (1~5번)

![](/image_SQL/5-9.PNG)  


![](/image_SQL/5-10.PNG)  

![](/image_SQL/5-11.PNG)  

![](/image_SQL/5-12.PNG)  

![](/image_SQL/5-13.PNG)  

![](/image_SQL/5-14.PNG)  


![](/image_SQL/5-15.PNG)  




## 4-6 조건문 함수  

**조건문**   
- 만약 특정 조건이 충족되면, 어떤 행동을 하자  
- 특정 조건이 참일때 A,  아니면 B
- 조건에 따른 분기 처리가 필요한 경우 
- 조건에 따라 다른 값을 표시하고 싶을 때 사용  

조건문을 사용하는 방법 
- 1) CASE WHEN
- 2) IF   

조건문 함수가 사용되는 이유 
- 데이터 분석을 하다보면, 특정 카테고리를 하나로 합치는 전처리가 필요할 수 있음  


**WHY?** 
1. 데이터 저장과 분석하는 쪽이 나뉨
2. 분석할 때 필요한 부분에서 조건 설정해서 변경하는 것이 유용 
3. 저장할 때부터 특정 카테고리를 합쳐서 저장하면, 쪼개서 보고 싶을 때 볼 수 없음  

## 1) CASE WHEN 
- 여러 조건이 있을 경우 사용. **순서주의**  



![](/image_SQL/5-16.PNG)  


![](/image_SQL/5-17.PNG)  



- 조건1, 조건2에 둘 다 해당하면 앞선 순서를 다름  

- 문자열 함수(특정 단어 추출)에서 이슈가 자주 발생  


## 2) IF

단일 조건일 경우 유용 


- 문법 :  IF(조건문, True일 때의 값, False일 때의 값) AS 새로운 컬럼 이름 

## 조건문 함수 연습 문제 (1~6번)

![](/image_SQL/5-18.PNG)  

![](/image_SQL/5-19.PNG)  

![](/image_SQL/5-20.PNG)  

![](/image_SQL/5-21.PNG)  

![](/image_SQL/5-22.PNG)  

![](/image_SQL/5-23.PNG)  

![](/image_SQL/5-24.PNG)  

