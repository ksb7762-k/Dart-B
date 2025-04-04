# 📘  캐글 필사 개념 정리 (Pandas, Seaborn, 인코딩 등)

---

## 1️⃣ `describe()`와 `include` 옵션

- `describe()`는 기본적으로 **숫자형 열**에 대한 통계 정보를 보여줌
- `describe(include='all')`: **모든 타입의 열**을 포함한 요약 통계 출력
- `describe(include=['O'])`: **오브젝트 타입(object)** 열만 따로 보기

```python
train_df.describe(include=['O'])  # 문자열/범주형만 요약
```

💡 *특정 타입의 컬럼만 보면 새로운 인사이트를 발견할 수 있음!*

---

## 2️⃣ `groupby(as_index=...)` 옵션

### 🔹 `as_index=True` (기본값)

- 그룹화한 컬럼이 **인덱스**로 설정됨

```python
df.groupby('Sex').mean()  # Sex가 인덱스로 사용됨
```

### 🔹 `as_index=False`

- 그룹화한 컬럼이 **일반 열(column)** 으로 유지되어 **가공이 더 쉬움**

```python
df.groupby('Sex', as_index=False).mean()
```

---

## 3️⃣ 정규 표현식과 `str.extract()`

```python
dataset.Name.str.extract(' ([A-Za-z]+)\.', expand=False)
```

- 정규 표현식 `' ([A-Za-z]+)\.'`:
  - 이름에서 Mr, Miss, Dr 같은 **호칭(title)** 만 추출
- `expand=False`: 결과를 **Series(1차원)** 로 반환  
- `expand=True`: 결과를 **DataFrame(2차원)** 으로 반환

---

## 4️⃣ Series vs DataFrame

| 구분 | 설명 |
|------|------|
| Series | 1차원, 하나의 열을 가진 데이터 |
| DataFrame | 2차원, 여러 행과 열로 구성된 표 형식 |
| 관계 | **Series는 DataFrame의 구성 요소** 중 하나 |

---

## 5️⃣ ✅ 인코딩의 종류

### 🔹 1. Label Encoding

- 각 범주(category)에 고유한 숫자를 부여  
- 예: `"male" → 0`, `"female" → 1`

**⚠️ 단점**: 숫자 간의 **순서/크기 의미**가 생겨, 일부 모델에서는 문제 발생 가능

---

### 🔹 2. One-Hot Encoding

- 범주별로 **별도의 열(column)** 생성  
- 해당 열만 1, 나머지는 0

예: `"male"` → `[1, 0]`, `"female"` → `[0, 1]`

**✅ 순서 정보가 사라져서 더 안전함**

---

## 6️⃣ Seaborn `FacetGrid`

```python
g = sns.FacetGrid(train_df, col='Survived')
g.map(plt.hist, 'Age', bins=20)
```

- `Survived` 값에 따라 데이터를 나누고,  
- 각 그룹(생존자/비생존자)에 대해 **Age 히스토그램** 시각화

---

### 🧩 FacetGrid란?

- Seaborn의 **하위 그룹별 시각화 도구**
- 데이터를 그룹화해서, **각 그룹마다 독립적인 그래프**를 나란히 보여줌
- `FacetGrid.map()`은 **모든 그래프(facet)에 동일한 시각화 함수**만 적용 가능

> 📌 `map()`으로는 **다른 facet마다 서로 다른 시각화 함수**는 적용 불가

---




| 방법                  | 각 facet에 다른 시각화 가능? | 유연성   | 추천 용도                  |
|-----------------------|-----------------------------|----------|-----------------------------|
| `FacetGrid.map()`     | ❌ 불가능                    | 제한적   | 같은 시각화를 반복할 때     |
| `FacetGrid.axes` 접근 | ✅ 가능                      | 높음     | 커스터마이징이 필요할 때   |
| `plt.subplots()`      | ✅ 가능                      | 매우 높음 | 완전히 자유롭게 그릴 때    |




### 🎯 Seaborn의 `FacetGrid.map()` 함수란?

`FacetGrid.map(func, *args, **kwargs)`

- **`func`**: 각 서브플롯(그래프)에 적용할 함수  
  예: `plt.hist`, `sns.scatterplot` 등

- **`*args`**: `func`에 전달할 인자  
  예: `'Age'`, `'Fare'` 등 **컬럼명들**

- **`**kwargs`**: 추가로 전달할 키워드 인자  
  예: `bins=20`, `color='blue'` 등


### 🧠 정리

| map() 종류              | 기능                   | 예시                                      |
|-------------------------|------------------------|--------------------------------------------|
| Python 기본 `map()`     | 함수 반복 적용         | `map(lambda x: x+1, list)`                |
| Pandas `map()`          | 값 치환 (매핑)         | `df['col'].map({'A': 1, 'B': 2})`         |
| Seaborn `FacetGrid.map()` | 그래프마다 함수 적용 | `FacetGrid.map(plt.hist, 'Age')`         |

✅ alpha란?  
alpha는 그래픽 요소의 투명도(불투명도)를 조절하는 매개변수

🎯 간단하게 말하면:
alpha = 1.0 → 완전히 불투명 (진하게 표시됨)

alpha = 0.0 → 완전히 투명 (보이지 않음)

alpha = 0.5 → 반투명 (겹치는 부분이 보이도록)


### 🎯 `height`와 `aspect`의 의미

Seaborn의 `FacetGrid`에서 그래프 하나(각 서브플롯)의 크기는 두 가지로 결정됨
```python
FacetGrid(..., height=세로크기, aspect=가로비율)
```

---

#### ✅ `height`

- 각 서브플롯의 **세로 크기**
- 단위: **인치 (inch)**
- 예: `height=2.2` → 세로 길이는 **2.2인치**

---

#### ✅ `aspect`

- **세로에 대한 가로의 비율 (aspect ratio)**
- 실제 가로 길이 = `height × aspect`
- 예:  
  `aspect=1.6`이고 `height=2.2`라면  
  → 가로 = `1.6 × 2.2` = **3.52인치**

---

리스트에 df를 담을 수 있다는 것을 처음 알았다. 

# 🧩 pandas `combine` 메서드 정리



## ✅ 1. 기본 개념

`combine()`은 pandas에서 두 개의 `Series` 또는 `DataFrame`을 **요소 단위로 비교/계산하여 결합**하는 메서드

```python
Series.combine(other, func)
DataFrame.combine(other, func)
```

- `other`: 비교할 대상 (`Series` 또는 `DataFrame`)
- `func`: 두 값을 받아 처리하는 함수 (`max`, `min`, 사용자 정의 함수 등)

---

## ✅ 2. Series 예제

```python
import pandas as pd

s1 = pd.Series([10, 20, 30])
s2 = pd.Series([15, 18, 25])

result = s1.combine(s2, func=max)
print(result)
```

**결과:**

```
0    15
1    20
2    30
dtype: int64
```

---

## ✅ 3. 사용자 정의 함수 활용

```python
def weighted_avg(x, y):
    return x * 0.6 + y * 0.4

result = s1.combine(s2, weighted_avg)
print(result)
```

**결과:**

```
0    12.0
1    19.2
2    27.0
dtype: float64
```

---

## ✅ 4. DataFrame 예제

```python
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [10, 20], 'B': [30, 40]})

df_combined = df1.combine(df2, lambda s1, s2: s1 + s2)
print(df_combined)
```

**결과:**

```
    A   B
0  11  33
1  22  44
```

---

## ✅ 5. `combine_first()` 와의 차이점

| 메서드 | 역할 |
|--------|------|
| `combine()` | 두 값이 모두 존재할 때, 함수를 적용하여 결합 |
| `combine_first()` | NaN 값이 있는 위치에 다른 DataFrame의 값을 채움 |

```python
df1.combine_first(df2)
```

---

## ✅ 6. 활용 예시 요약

| 상황 | 예시 |
|------|------|
| 최대값 선택 | `s1.combine(s2, max)` |
| 평균 또는 가중치 계산 | 사용자 정의 함수 |
| 결측값 채우기 | `combine_first()` 사용 |
| 여러 DataFrame 전처리 | `for dataset in [df1, df2]: ...` 구조와 함께 사용 |

---

# 📊 Seaborn `pairplot()` 함수 정리

`pairplot()`은 여러 변수 간의 관계를 한 번에 시각화해주는 **산점도 행렬**(scatter plot matrix)을 생성하는 함수

---

## ✅ 기본 문법

```python
sns.pairplot(data, **kwargs)
```

- `data`: DataFrame 형식의 데이터
- `**kwargs`: 다양한 설정 옵션 (예: `hue`, `diag_kind`, `plot_kws` 등)

---

## 🧠 주요 기능

- 각 변수 쌍에 대해 **산점도**를 그림
- 대각선에는 **변수의 분포**를 그림 (`hist` 또는 `kde`)
- `hue` 인자를 통해 **범주형 컬럼**을 기준으로 색상을 다르게 지정 가능
- EDA(탐색적 데이터 분석)에서 **변수 간 관계를 파악하는 데 매우 유용**

---

## 🎯 주요 파라미터 정리

| 파라미터 | 설명 |
|----------|------|
| `hue` | 범주형 변수에 따라 점의 색상을 다르게 지정 |
| `diag_kind` | 대각선에 표시할 분포 유형 (`'kde'` 또는 `'hist'`) |
| `palette` | 색상 팔레트 지정 (`'seismic'`, `'Set1'`, `'husl'` 등) |
| `plot_kws` | 산점도 관련 옵션 전달 (`s`, `alpha`, `color` 등) |
| `diag_kws` | 대각선 분포 그래프 옵션 전달 (예: `shade=True`) |
| `corner` | `True`로 설정 시 좌측 하단만 표시 (중복 제거) |
| `height` | 각 subplot의 크기 지정 (버전에 따라 `size`) |

---

## 🧪 예제 코드

```python
import seaborn as sns
import matplotlib.pyplot as plt

# 예제 데이터셋 불러오기
df = sns.load_dataset("iris")

# pairplot 생성
sns.pairplot(df, hue='species', diag_kind='kde', plot_kws=dict(s=20), palette='husl')
plt.show()
```

---

## 🔍 결과 해석

- 모든 변수 쌍의 산점도 → 변수 간 관계 확인 가능
- 대각선은 각 변수의 분포 → 데이터가 어떻게 퍼져 있는지 파악
- `hue='species'` → 각 종(species)에 따라 색상 다르게 표시됨

---

## 💡 사용 팁

- 너무 많은 변수를 한꺼번에 넣으면 **그래프가 복잡**해질 수 있으므로, 주요 변수만 선택해서 시각화하는 것이 좋음
- `corner=True` 옵션을 사용하면 **하단 삼각형 영역만 출력**돼서 더 깔끔한 시각화가 가능

```python
sns.pairplot(df, hue='species', corner=True)
```

---

## 📌 요약

| 목적 | 설명 |
|------|------|
| 변수 간 관계 시각화 | 산점도 행렬 생성 |
| 분포 확인 | 대각선에 KDE/히스토그램 표시 |
| 색상 구분 | 범주형 변수로 그룹 시각화 |
| 실습 활용도 | EDA(탐색적 데이터 분석)에 매우 유용 |

---

## 🔹 `plot_kws=dict(s=10)` 

### ✅ 기본 의미

```python
plot_kws = dict(s=10)
```

- `plot_kws`: `sns.pairplot()`에서 **산점도(scatter plot)**의 속성을 조절할 때 사용하는 인자
- `dict`: Python의 **딕셔너리(dictionary)** 자료형
- `s=10`: **점의 크기(size)** 를 10으로 설정

👉 즉, **산점도의 점 크기를 10으로 설정**한다는 뜻

---

### 🧠 왜 `dict`를 쓰는가?

- `plot_kws`는 내부적으로 `sns.scatterplot()` 함수에 전달
- 여러 시각화 옵션을 한꺼번에 넘기기 위해 **딕셔너리 형태**로 작성

예:

```python
plot_kws = dict(s=10, alpha=0.6, color='red')
```

- `s=10`: 점 크기
- `alpha=0.6`: 투명도
- `color='red'`: 점 색상

---

### 🧪 예제 코드

```python
import seaborn as sns
import pandas as pd

# 예제 데이터
df = sns.load_dataset("iris")

# pairplot에 plot_kws 적용
sns.pairplot(df, hue='species', plot_kws=dict(s=10))
```

---

### ✅ 정리 표

| 항목 | 설명 |
|------|------|
| `plot_kws` | 산점도 관련 설정 전달 인자 |
| `dict` | 파이썬 딕셔너리 자료형 |
| `s=10` | 점의 크기를 10으로 설정 |
| 활용 | 점 크기, 색상, 투명도 등 설정 가능 |



### 🔍 시각적 차이

| 설정 | 결과 |
|------|------|
| `shade=False` | 곡선만 그려짐 (기본값) |
| `shade=True` | 곡선 아래에 색이 칠해짐 → 더 강조됨 |

---

