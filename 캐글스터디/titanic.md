1. describe()나 describe(include=’all’) 이외에 오브젝트 타입만 따로 볼 수 있다는 것을 처음알았다.  ex) train_df.describe(include=['O']) 

이처럼 칼럼을 나누어서 보면 생각지도 못했던 인사이트를 발견할 수 있다는 것을 깨달았다. 

1. **as_index : 집계 결과에서 그룹화한 컬럼을 인덱스로 사용할지 여부**를 설정할 때 쓰임.

🔹 `as_index=True` (기본값)

- 그룹화한 컬럼이 **인덱스**로 설정
- 결과 DataFrame의 **행 인덱스에 그룹화된 컬럼이 위치**
- 

🔹 `as_index=False`

- 그룹화한 컬럼이 인덱스가 아닌 **일반 열(column)** 로 유지
- 데이터를 다루기 더 쉬운 형태로 사용

dataset.Name.str.extract(' ([A-Za-z]+)\.', expand=False)
이 정규 표현식은 괄호 ( )로 감싸진 부분을 기준으로 문자열에서 값을 추출
이때 expand는 결과를 데이터프레임으로 반환할지, 시리즈(Series)로 반환할지를 정하는 역할
expand=True (기본값) 결과를 DataFrame으로 반환
expand=False 결과를 Series로 반환

series와 dataframe의 차이

Series는 1개의 열만 있는 데이터 (1차원)

DataFrame은 여러 열과 행으로 구성된 표 형태의 데이터 (2차원)

즉, Series는 DataFrame의 구성 요소 중 하나

✅ 인코딩의 종류
1. Label Encoding (레이블 인코딩)
각 범주(category)에 숫자를 부여

예: "male" → 0, "female" → 1

단점: 숫자의 크기(순서) 가 의미를 가질 수 있어, 일부 모델에 부정적 영향을 줄 수 있음

2. One-Hot Encoding (원-핫 인코딩)
각 범주를 별도의 열(Column) 로 만들고, 해당하는 위치에만 1, 나머지는 0

예: "male" → [1, 0], "female" → [0, 1]

순서의 영향을 없애는 방법

🧩 FacetGrid란?

FacetGrid는 Seaborn 라이브러리의 시각화 도구로, 데이터의 하위 그룹(subsets)을 나누어 각각의 그래프를 그릴 수 있도록 해주는 기능


| 방법                  | 각 facet에 다른 시각화 가능? | 유연성   | 추천 용도                  |
|-----------------------|-----------------------------|----------|-----------------------------|
| `FacetGrid.map()`     | ❌ 불가능                    | 제한적   | 같은 시각화를 반복할 때     |
| `FacetGrid.axes` 접근 | ✅ 가능                      | 높음     | 커스터마이징이 필요할 때   |
| `plt.subplots()`      | ✅ 가능                      | 매우 높음 | 완전히 자유롭게 그릴 때    |


### 🧠 정리

| map() 종류              | 기능                   | 예시                                      |
|-------------------------|------------------------|--------------------------------------------|
| Python 기본 `map()`     | 함수 반복 적용         | `map(lambda x: x+1, list)`                |
| Pandas `map()`          | 값 치환 (매핑)         | `df['col'].map({'A': 1, 'B': 2})`         |
| Seaborn `FacetGrid.map()` | 그래프마다 함수 적용 | `FacetGrid.map(plt.hist, 'Age')`         |
