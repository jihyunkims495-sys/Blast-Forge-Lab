# [머신러닝 기초] 2장 1강: 선형 회귀 모델과 오차 평가지표

## 학습 목표

- 선형 회귀의 예측 메커니즘과 MSE, MAE 평가지표의 특성을 설명할 수 있다.
- Scikit-learn을 활용하여 단순 선형 회귀 모델을 구현하고 모델의 오차를 계산할 수 있다.

## 사용 프로그램

- VS Code
- uv

## 사용 라이브러리

- Python
- Scikit-learn
- Pandas
- Matplotlib

---

## 1. 선형 회귀와 오차

### 1.1 선형 회귀(Linear Regression)

선형 회귀는 입력값과 타겟 사이의 관계를 하나의 직선으로 표현하여 새로운 값을 예측하는 머신러닝 기법이다.

기본 식은 다음과 같다.

```text
y_hat = w * x + b
```

- `y_hat`: 모델의 예측값
- `x`: 입력값(Feature)
- `w`: 가중치(Weight), 직선의 기울기
- `b`: 편향(Bias), 직선의 절편

머신러닝에서 학습이란 데이터를 바탕으로 **오차가 가장 작아지는 w와 b를 찾는 과정**이라고 볼 수 있다.

### 1.2 오차(Error), 손실 함수(Loss Function), 손실값(Loss)

- **오차(Error)**: 개별 데이터에서 실제값과 예측값의 차이
- **손실 함수(Loss Function)**: 여러 오차를 하나의 기준으로 계산하는 공식
- **손실값(Loss)**: 현재 예측 결과를 손실 함수에 넣어 계산한 실제 숫자

모델은 학습하면서 손실값이 작아지는 방향으로 파라미터를 조정한다.

## 2. MSE와 MAE

### 2.1 평균 제곱 오차(MSE)

```text
MSE = 평균((실제값 - 예측값)^2)
```

오차를 제곱하기 때문에 큰 오차에 더 큰 패널티를 준다.

- 장점: 큰 오차를 강하게 억제
- 특징: 이상치에 민감
- 최적화 측면: 매끄럽고 미분하기 쉬움

### 2.2 평균 절대 오차(MAE)

```text
MAE = 평균(|실제값 - 예측값|)
```

오차의 절대값을 사용한다.

- 장점: 실제 타겟과 같은 단위라 해석이 직관적
- 특징: MSE보다 이상치에 덜 민감

### 2.3 MSE와 MAE 비교

| 항목 | MSE | MAE |
| --- | --- | --- |
| 계산 방식 | 오차 제곱 평균 | 오차 절대값 평균 |
| 큰 오차 반응 | 매우 큼 | 선형적으로 증가 |
| 이상치 민감도 | 높음 | 상대적으로 낮음 |
| 해석 단위 | 원래 단위의 제곱 | 원래 단위와 동일 |
| 미분 | 매끄러움 | 오차 0 지점에서 미분 불가능 |

> 참고: MAE는 이상치에 비교적 강건하지만, 학습 과정에서 항상 MSE보다 우월하다는 의미는 아니다. 목적과 데이터 특성에 따라 선택한다.

## 3. 미분의 의미

미분은 현재 위치에서 함수가 어느 방향으로 얼마나 빠르게 변하는지를 나타낸다.

- 미분값 < 0: 오른쪽으로 이동할수록 값이 감소
- 미분값 > 0: 오른쪽으로 이동할수록 값이 증가
- 미분값 = 0: 기울기가 평평한 지점

> 교안 보정: 최저점에서의 미분값은 **0**이다. 양수가 아니다.

미분값의 부호는 이동 방향을 결정하는 데 쓰이고, 절대값의 크기는 현재 위치의 경사 정도를 나타낸다.

## 4. 실습 환경 준비

```bash
uv init chapter02
cd chapter02
uv add scikit-learn pandas matplotlib numpy ipykernel
```

VS Code에서 `01.ipynb`를 만들고 프로젝트의 `.venv` 커널을 선택한다.

## 5. 주택 가격 예측 선형 회귀 구현

### 5.1 데이터 불러오기

```python
import pandas as pd
import matplotlib.pyplot as plt


df = pd.read_csv('usa_housing.csv')
df.head()
```

### 5.2 데이터 필터링

```python
latest_year = df['YearBuilt'].max()
df = df[(df['YearBuilt'] > 2015) & (df['CrimeRate'] < 40)]
df.head()
```

`latest_year`를 계산했지만 아래 필터에서는 실제로 사용하지 않는다. 필요 없다면 제거해도 된다.

### 5.3 데이터 분포 확인

```python
plt.figure(figsize=(8, 5))
plt.scatter(df['SquareFeet'], df['Price'], alpha=0.5)
plt.title('House Area vs Price')
plt.xlabel('Square Feet (Area)')
plt.ylabel('Price ($)')
plt.grid(True)
plt.show()
```

면적이 넓어질수록 가격이 대체로 증가하는 패턴이 보인다면 선형 회귀 적용을 검토할 수 있다.

### 5.4 Feature와 Target 분리

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error

X = df[['SquareFeet']]
y = df['Price']
```

Scikit-learn은 입력 Feature `X`를 일반적으로 2차원 배열 형태로 받기 때문에 `[['SquareFeet']]`처럼 사용한다.

### 5.5 모델 학습

```python
model = LinearRegression()
model.fit(X, y)
```

### 5.6 예측

```python
y_pred = model.predict(X)
y_pred
```

### 5.7 오차 계산

```python
mse = mean_squared_error(y, y_pred)
mae = mean_absolute_error(y, y_pred)

print(f"컴퓨터가 찾은 기울기(w): {model.coef_}")
print(f"컴퓨터가 찾은 기본값(b): {model.intercept_:.2f}")
print(f"오차 제곱 평균(MSE): {mse:.2f}")
print(f"오차 절대값 평균(MAE): {mae:.2f}")
```

### 5.8 회귀선 시각화

```python
plt.figure(figsize=(8, 5))
plt.scatter(X, y, alpha=0.5, label='Actual Data')
plt.plot(X, y_pred, linewidth=3, label='Regression Line')
plt.title('Linear Regression Prediction')
plt.xlabel('Square Feet (Area)')
plt.ylabel('Price ($)')
plt.legend()
plt.grid(True)
plt.show()
```

## 6. 개념 체크

### Q1

선형 회귀 모델이 학습을 통해 찾는 것은?

**정답: (2) 최적의 기울기(w)와 편향(b)**

### Q2

"평균적으로 2천 달러 정도 틀린다"처럼 실제 단위로 설명하기 쉬운 지표는?

**정답: (2) MAE**

---

# [머신러닝 기초] 2장 2강: 경사하강법, 옵티마이저 및 데이터 분할

## 학습 목표

- 경사하강법이 손실을 최소화하는 기본 최적화 메커니즘임을 설명할 수 있다.
- 미분을 이용한 가중치 업데이트가 딥러닝 역전파의 기초가 됨을 이해할 수 있다.
- 학습률을 조정하며 최적화 과정을 이해하고 데이터를 훈련/검증/테스트 세트로 분할할 수 있다.

## 사용 프로그램

- VS Code
- Jupyter Notebook

## 사용 라이브러리

- Python 3.13
- Scikit-learn
- NumPy
- Pandas
- Matplotlib

---

## 1. 경사하강법(Gradient Descent)

경사하강법은 손실 함수의 값을 최소화하기 위해 기울기의 반대 방향으로 파라미터를 조금씩 업데이트하는 최적화 알고리즘이다.

### 1.1 핵심 업데이트 공식

```text
w_new = w_old - learning_rate * gradient
```

수식으로는 다음과 같다.

```text
w_new = w_old - α * ∂J/∂w
```

- `w_old`: 현재 가중치
- `w_new`: 업데이트된 가중치
- `α`: 학습률(Learning Rate)
- `J`: 손실 함수
- `∂J/∂w`: w를 변화시켰을 때 손실이 얼마나 변하는지를 나타내는 기울기

기울기는 손실이 증가하는 방향을 알려주므로, 손실을 줄이려면 반대 방향으로 움직여야 한다. 그래서 공식에 `-`가 붙는다.

## 2. 옵티마이저와 학습률

### 2.1 옵티마이저(Optimizer)

옵티마이저는 손실을 줄이는 방향으로 모델 파라미터를 업데이트하는 방법 또는 알고리즘이다.

경사하강법은 가장 기본적인 최적화 방식이고, 이를 바탕으로 SGD, Momentum, Adam 등 다양한 옵티마이저가 발전했다.

### 2.2 학습률(Learning Rate)

학습률은 한 번의 업데이트에서 파라미터를 얼마나 크게 이동시킬지 결정한다.

| 학습률 상태 | 결과 |
| --- | --- |
| 너무 큼 | 최저점을 지나치거나 발산 가능 |
| 너무 작음 | 수렴 속도가 매우 느려짐 |
| 적절함 | 안정적으로 손실 감소 |

> `Undershooting`은 머신러닝에서 표준적으로 널리 쓰이는 용어는 아니다. 보통 학습률이 너무 작아 **수렴이 느리다**고 표현하는 편이 정확하다.

## 3. 모델 파라미터와 하이퍼파라미터

### 모델 파라미터(Model Parameter)

학습을 통해 모델이 직접 찾는 값이다.

- 가중치 `w`
- 편향 `b`

### 하이퍼파라미터(Hyperparameter)

학습 전에 사람이 정하는 설정값이다.

- 학습률
- Epoch 수
- 배치 크기
- 정규화 강도 등

## 4. 지역 최솟값(Local Minimum)

### 볼록 함수(Convex Function)

최솟값이 하나이며 경사하강법이 전역 최솟값으로 수렴하기 쉬운 형태다.

### 비볼록 함수(Non-convex Function)

여러 개의 봉우리와 골짜기가 존재할 수 있다. 딥러닝의 손실 함수는 대체로 비볼록 형태이므로 최적화가 더 복잡하다.

SGD, Momentum, Adam 등의 방법은 실제 학습을 더 효율적으로 만드는 데 사용된다.

## 5. 데이터 분할(Data Split)

데이터는 보통 훈련, 검증, 테스트 세트로 나눈다.

| 데이터 | 역할 | 예시 비율 |
| --- | --- | --- |
| Train | 모델 파라미터 학습 | 60% |
| Validation | 하이퍼파라미터 조정 및 중간 평가 | 20% |
| Test | 최종 일반화 성능 평가 | 20% |

테스트 세트는 모델 개발 과정에서 반복적으로 들여다보지 않는 것이 중요하다.

### train_test_split 주요 옵션

- `test_size=0.2`: 테스트 비율 20%
- `random_state=42`: 동일한 분할 재현
- `shuffle=True`: 분할 전에 데이터 섞기
- `stratify=y`: 분류 문제에서 클래스 비율 유지

> `stratify=y`는 주로 **분류 문제**에서 사용한다. 연속값을 예측하는 일반적인 회귀 문제에는 그대로 적용하지 않는 것이 보통이다.

## 6. 스케일링(Scaling)

Feature마다 숫자 범위가 크게 다르면 일부 최적화 알고리즘의 학습이 불안정하거나 느려질 수 있다.

### 6.1 MinMaxScaler

```text
x_scaled = (x - min) / (max - min)
```

일반적으로 데이터를 0~1 범위로 변환한다.

### 6.2 StandardScaler

```text
z = (x - mean) / std
```

평균을 0, 표준편차를 1로 맞춘다.

### 분산, 표준편차, Z-score

- 분산: 평균을 기준으로 데이터가 얼마나 퍼져 있는지 나타내는 값
- 표준편차: 분산의 제곱근
- Z-score: 평균에서 표준편차 몇 배만큼 떨어져 있는지 나타내는 값

## 7. 데이터 스케일링 및 분할 실습

```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler, StandardScaler
import matplotlib.pyplot as plt
import platform

if platform.system() == 'Darwin':
    plt.rc('font', family='AppleGothic')
elif platform.system() == 'Windows':
    plt.rc('font', family='Malgun Gothic')

plt.rcParams['axes.unicode_minus'] = False
```

### 데이터 불러오기

```python
df = pd.read_csv('usa_housing.csv')
df.head()
```

### Feature와 Target 준비

```python
X_sqft = df['SquareFeet'].values.reshape(-1, 1)
y_price = df['Price'].values.reshape(-1, 1)
```

### MinMaxScaling

```python
scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()

X_scaled = scaler_X.fit_transform(X_sqft).flatten()
y_scaled = scaler_y.fit_transform(y_price).flatten()
```

> 실무에서는 데이터 누수(Data Leakage)를 막기 위해 **훈련/검증/테스트로 먼저 나눈 뒤, scaler를 훈련 세트에만 fit**하고 나머지 세트에는 transform만 적용하는 것이 원칙이다.

### 60/20/20 분할

```python
X_train_val, X_test, y_train_val, y_test = train_test_split(
    X_scaled, y_scaled, test_size=0.2, random_state=42
)

X_train, X_valid, y_train, y_valid = train_test_split(
    X_train_val, y_train_val, test_size=0.25, random_state=42
)
```

두 번째 분할에서 80%의 25%가 전체의 20%가 되므로 결과적으로 Train 60%, Validation 20%, Test 20%가 된다.

## 8. 직접 구현하는 경사하강법

### 초기값 설정

```python
weight = 0.0
bias = 0.0
learning_rate = 0.1
epochs = 200

train_losses = []
valid_losses = []
history_w = []

N_train = len(X_train)
```

### 학습 루프

```python
for epoch in range(epochs):
    y_pred_train = weight * X_train + bias
    train_loss = np.mean((y_pred_train - y_train) ** 2)
    train_losses.append(train_loss)

    y_pred_valid = weight * X_valid + bias
    valid_loss = np.mean((y_pred_valid - y_valid) ** 2)
    valid_losses.append(valid_loss)

    history_w.append(weight)

    dw = (2 / N_train) * np.sum((y_pred_train - y_train) * X_train)
    db = (2 / N_train) * np.sum(y_pred_train - y_train)

    weight -= learning_rate * dw
    bias -= learning_rate * db
```

이 코드는 MSE를 손실 함수로 사용하고, 직접 미분한 기울기 `dw`, `db`를 이용해 `w`, `b`를 업데이트한다.

## 9. 학습 결과 해석

훈련 손실과 검증 손실이 함께 감소하면서 비슷한 수준에서 안정되면 일반적으로 학습이 잘 진행되고 있다고 볼 수 있다.

반면 훈련 손실은 계속 감소하는데 검증 손실이 다시 증가한다면 과적합을 의심할 수 있다.

## 10. 개념 체크

### Q1

큰 숫자 범위를 0~1로 줄여주는 대표 도구는?

**정답: (3) MinMaxScaler**

### Q2

Train/Validation/Test로 나누는 가장 중요한 이유는?

**정답: (2) 학습과 평가를 분리하여 과적합을 확인하고 일반화 성능을 평가하기 위해서**

---

## 핵심 연결 구조

```text
데이터
  ↓
선형 회귀 모델
  ↓
예측값 y_hat = wx + b
  ↓
실제값과 비교
  ↓
MSE / MAE로 오차 측정
  ↓
미분으로 Gradient 계산
  ↓
경사하강법으로 w, b 업데이트
  ↓
Train / Validation으로 학습 상태 점검
  ↓
Test 데이터로 최종 일반화 성능 평가
```

## 오늘의 한 줄 정리

**머신러닝의 학습은 예측 오차를 계산하고, 미분으로 손실이 줄어드는 방향을 찾은 뒤, 경사하강법으로 파라미터를 반복해서 수정하는 과정이다.**
