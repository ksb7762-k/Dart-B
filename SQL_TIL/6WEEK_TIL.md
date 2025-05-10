# 5. JOIN 

**SQL JOIN  : 서로 다른 데이터 테이블을 연결하는 것**   

## 포켓몬으로 JOIN 이해하기 

트레이너가 포획한 포켓몬 기준으로 트레이너 데이터를 연결하기 (JOIN)    

연결할 수 있는 Key = **traier_id, id**  


![](/image_SQL/6-1.PNG)  




2개의 테이블에서 공통으로 가지고 있는 KEY를 기준으로 테이블을 붙인다! 

**추가로** pokemon_id와 포켓몬 테이블의 id를 기준으로 합칠 수도 있음! 


![](/image_SQL/6-2.PNG)  


## JOIN을 해야하는 이유 - 데이터 저장되는 형태에 대한 이해
- 관계형 데이터베이스(RDBMS) 설계 시 정규화 과정을 거침
- 정규화는 **중복을 최소화하게 데이터를 구조화**
- User Table은 유저 데이터만, Order Table은 주문 데이터만 
- 따라서 데이터를 다양한 Table에 저장해서 필요할 때 JOIN해서 사용 

## 5-3 다양한 JOIN 방법 

- (INNER) JOIN : 두 테이블의 **공통**요소만 연결 
- LEFT/RIGHT (OUTER) JOIN : **왼쪽/오른쪽** 테이블 **기준**으로 연결 
- FULL (OUTER) JOIN : **양쪽** 기준으로 연결  
- CROSS JOIN  : 두 테이블의 각각의 **요소**를 **곱하기**  


![](/image_SQL/6-3.PNG)  



## 5-4 JOIN 쿼리 작성하기  


**흐름** 


![](/image_SQL/6-4.PNG)  



## SQL JOIN 문법  


FROM 하단에 JOIN할 Table을 작성하고 ON 뒤에 공통된 컬럼(Key)을 작성  

  **(CROSS JOIN은 ON 필요없음)**  


![](/image_SQL/6-5.PNG)  



## NULL이 대체 뭐죠?

- NULL : 값이 없음, 알 수 없음
- 0이나 공백과 다르게 아예 없는 것
- JOIN에선 연결할 값이 없는 경우 나타남  



![](/image_SQL/6-6.PNG)  


## JOIN 연습문제 (1~5번)  


![](/image_SQL/6-7.PNG)  



![](/image_SQL/6-8.PNG)  


![](/image_SQL/6-9.PNG)  


![](/image_SQL/6-10.PNG)  


![](/image_SQL/6-11.PNG)  
  


![](/image_SQL/6-12.PNG)  

 

