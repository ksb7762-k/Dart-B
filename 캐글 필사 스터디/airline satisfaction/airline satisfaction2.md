# FROM member's code 

plt.figure(figsize=(10,5), dpi = 100)  

## dpi란?

- `dpi(dots per inch)`는  1인치(2.54cm) 안에 몇 개의 점(dot)을 찍을 것인지 나타내는 단위
- `dpi`가 클수록 해상도가 높고 이미지가 더 선명해짐  

## 모델링에서 데이터 분할 방법 쉽게 요약

- 일반적으로 데이터셋은 `train.csv`랑 `test.csv`로 제공됨  
- 여기서 `train.csv`는 모델 학습용, `test.csv`는 평가 또는 제출용임  
- 하지만 모델 개발 과정에서는 `train.csv`도 다시 나눠야 함  
- 왜냐면 모델 성능을 검증하고 튜닝하려면 "알고 있는 데이터 안에서" 테스트가 필요함

---

### 1. 홀드아웃 (Hold-Out)

- `train.csv`를 다시 훈련용과 검증용으로 나눔  
- 예: `train.csv` 중 80% → 학습, 20% → 검증  
- `from sklearn.model_selection import train_test_split`로 쉽게 나눌 수 있음  
- 장점: 빠름  
- 단점: 데이터 적을 땐 결과가 불안정할 수 있음

---

### 2. 교차 검증 (Cross Validation, CV)

- `train.csv`를 여러 조각으로 나눠서 여러 번 학습하고 평가함  
- 예: 5-Fold CV → 5개로 나눠서 번갈아가며 학습과 검증 반복  
- 장점: 더 안정적인 성능 확인 가능  
- 단점: 시간 오래 걸림  
- `sklearn.model_selection.KFold`나 `StratifiedKFold`로 가능

---

### 3. Stratified Split (계층 분할)

- 분류 문제에서 클래스 비율을 유지한 채로 train/valid로 나눔  
- 데이터 불균형 있을 때 특히 중요함  
- `StratifiedKFold`, `StratifiedShuffleSplit` 등으로 구현 가능

---

### 4. 시간 기반 분할 (Time Series Split)

- 시계열 데이터인 경우, 시간 순서를 고려해서 분할함  
- 과거 → 미래 순으로 나눠야 함 (랜덤 X)  
- `TimeSeriesSplit` 사용  
- 시계열 예측에서는 필수

---
