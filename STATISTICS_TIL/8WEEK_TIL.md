# chapter 13~14 

### Elastic Net: 개념과 동작 원리

Elastic Net은 회귀 분석에서 변수 선택과 정규화를 동시에 수행하는 선형 모델의 일종  

 Lasso(Least Absolute Shrinkage and Selection Operator)와 Ridge Regression(릿지 회귀)의 장점을 결합한 모델로, L1 규제(Lasso)와 L2 규제(Ridge)를 동시에 사용



#### 동작 메커니즘

- Lasso의 L1 페널티는 변수 선택 효과를 가져옴. 일부 계수를 정확히 0으로 만들어 불필요한 변수를 제거.

- Ridge의 L2 페널티는 계수를 작게 만들어 다중공선성 문제를 완화. 계수를 0으로 만들지는 않음.

- Elastic Net은 L1과 L2의 절충 → 변수 선택 + 다중공선성 완화 모두 가능.


#### Elastic Net의 장점

- Lasso의 문제점 보완: Lasso는 p > n (변수 개수가 표본보다 많음) 상황에서 변수 선택이 불안정하거나, 강하게 상관된 변수 중 하나만 선택하는 경향. Elastic Net은 상관된 변수들을 함께 선택 가능.


- Ridge의 문제점 보완: Ridge는 모든 변수를 사용하지만, 불필요한 변수도 포함될 수 있음. Elastic Net은 일부 계수를 0으로 만들어 변수 선택도 가능.

#### Elastic Net의 활용 예

- 변수 선택이 필요한 고차원 데이터 (예: 유전자 데이터, 텍스트 데이터 등)에서 사용.

- 다중공선성 문제가 있는 데이터에서 유용.

- 머신러닝 파이프라인에서 특성 선택과 정규화를 동시에 적용할 때 적합.


#### 구현 (예: Scikit-Learn)

```python
from sklearn.linear_model import ElasticNet

model = ElasticNet(alpha=1.0, l1_ratio=0.5)
model.fit(X_train, y_train)
```

### 선형판별분석(LDA)와 이차판별분석(QDA) 개념과 원리

#### 1️⃣ 선형판별분석 (LDA: Linear Discriminant Analysis)

- 분류(classification) 문제 해결을 위한 지도학습 알고리즘

- 목표: 주어진 데이터의 클래스 간 분산을 최대화하고, 클래스 내 분산을 최소화하는 선형 판별 함수 찾기

- 가정:
  - 각 클래스는 공분산 행렬(Σ)이 동일함 (homoscedasticity)

  - 각 클래스는 정규분포(가우시안 분포) 따름

- 선형 결정 경계 생성 (hyperplane)

- 선형 함수라서 결정 경계는 직선/평면 형태

#### 2️⃣ 이차판별분석 (QDA: Quadratic Discriminant Analysis)


- LDA의 가정을 완화하여 클래스별로 다른 공분산 행렬 허용

- 각 클래스마다 고유한 공분산 행렬

- 따라서 더 유연한 결정 경계 가능 (이차 곡선 형태)

- 결정 경계는 이차 함수 형태 → 타원, 쌍곡선, 포물선 등의 경계 가능


#### 4️⃣ LDA와 QDA의 적용 사례

- LDA: 데이터가 잘 구분되며, 클래스별 분포의 형태(공분산 구조)가 비슷한 경우 (ex: 이진 분류의 금융 사기 탐지)
- QDA: 클래스 간 분포 형태가 다르거나 공분산의 차이를 활용할 수 있는 경우 (ex: 생물 종 분류)


#### 6️⃣ 구현 (예: Scikit-Learn)

```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis, QuadraticDiscriminantAnalysis

# LDA
lda = LinearDiscriminantAnalysis()
lda.fit(X_train, y_train)

# QDA
qda = QuadraticDiscriminantAnalysis()
qda.fit(X_train, y_train)

```

