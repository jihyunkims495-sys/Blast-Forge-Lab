# [머신러닝 기초] 1장 1강: 머신러닝의 이해

## 학습 목표

- 전통적 프로그래밍과 머신러닝의 개념적 차이 및 지도·비지도·강화학습의 메커니즘을 설명할 수 있다.
- 주어진 비즈니스 요구사항을 분석하여 적절한 머신러닝 문제 유형으로 분류할 수 있다.

---

## 이번에 배울 것

사람이 모든 규칙을 직접 코딩하는 대신, 컴퓨터가 데이터에서 패턴을 찾아 스스로 규칙을 만들어내는 것이 머신러닝의 핵심이다.

## 1. 머신러닝이란 무엇일까요?

### 1.1 전통적 프로그래밍 vs 머신러닝

| 구분 | 전통적 프로그래밍 | 머신러닝 |
| --- | --- | --- |
| 작동 원리 | 사람이 규칙을 직접 작성 | 컴퓨터가 데이터에서 패턴을 학습 |
| 입력과 출력 | 데이터 + 규칙 → 해답 | 데이터 + 해답 → 규칙(모델) |
| 장점 | 결과가 명확하고 설명이 쉬움 | 복잡한 패턴과 변화에 대응 가능 |
| 예시 | 급여 계산, 자판기 | 스팸 분류, 추천, 자율주행 |

머신러닝에서 학습된 규칙을 **모델(Model)** 이라고 부른다.

### 1.2 톰 미첼의 머신러닝 정의

> 컴퓨터가 어떤 작업(T)을 할 때, 경험(E)이 쌓일수록 성능(P)이 좋아진다면 학습하고 있다고 볼 수 있다.

- 작업(T): 스팸 분류, 체스 게임
- 경험(E): 이메일 데이터, 체스 대국 기록
- 성능(P): 정확도, 승률

## 2. 머신러닝의 3가지 학습 방식

### 2.1 지도 학습 (Supervised Learning)

정답인 **라벨(Label)** 이 포함된 데이터를 학습하는 방식이다.

- **분류(Classification)**: 정답이 범주인 문제
  - 예: 스팸/정상, 이탈/유지
- **회귀(Regression)**: 정답이 연속적인 숫자인 문제
  - 예: 집값, 매출액 예측

모델은 예측값과 실제 정답 사이의 오차를 계산하고, 오차를 줄이는 방향으로 가중치와 편향을 조정한다.

### 2.2 비지도 학습 (Unsupervised Learning)

정답 없이 데이터의 특징과 구조를 스스로 찾는 방식이다.

대표적인 예시는 **군집화(Clustering)** 다. 데이터 간 거리를 바탕으로 비슷한 데이터끼리 그룹을 만든다.

예: 구매 패턴을 기준으로 고객을 여러 그룹으로 나누기

### 2.3 강화 학습 (Reinforcement Learning)

환경과 상호작용하면서 행동(Action)을 선택하고, 보상(Reward)을 최대화하는 방향으로 학습한다.

예: 게임 AI, 자율주행, 광고 입찰 최적화

핵심은 당장의 보상뿐 아니라 미래에 얻을 수 있는 보상까지 고려하는 것이다.

### 2.4 어떤 학습법을 선택할까?

1. 정답(라벨)이 있는가?
   - 있다 → 지도 학습
     - 숫자 → 회귀
     - 범주 → 분류
2. 정답은 없지만 비슷한 것끼리 묶고 싶은가?
   - 비지도 학습(군집화)
3. 행동에 따른 보상/벌이 있고 상호작용하며 배우는가?
   - 강화 학습

### 실전 사례

| 사례 | 문제 유형 |
| --- | --- |
| 다음 달 고객 이탈 여부 예측 | 지도 학습 - 분류 |
| 다음 분기 매출액 예측 | 지도 학습 - 회귀 |
| 구매 패턴 기반 고객 그룹화 | 비지도 학습 - 군집화 |
| 광고 입찰가를 조절하며 클릭 보상 최대화 | 강화 학습 |

## 3. 개념 체크

### Q1

머신러닝의 특징을 가장 잘 설명한 것은?

**정답: (2)** 컴퓨터에게 데이터와 정답을 주면 컴퓨터가 스스로 둘 사이의 규칙을 찾는다.

### Q2

넷플릭스 시청 기록만으로 비슷한 취향의 사람을 묶는 학습법은?

**정답: (3) 비지도 학습**

## 핵심 키워드

- 머신러닝: 데이터에서 규칙과 패턴을 학습하는 기술
- 지도 학습: 정답이 있는 데이터로 학습
- 비지도 학습: 정답 없이 구조와 패턴 탐색
- 강화 학습: 보상을 최대화하도록 행동을 학습
- 분류: 범주 예측
- 회귀: 연속값 예측
- 피처(Feature): 모델이 입력으로 사용하는 단서
- 라벨/타겟(Label/Target): 모델이 맞춰야 하는 정답

---

# [머신러닝 기초] 1장 2강: 데이터 분석 기초

## 학습 목표

- 데이터 조작 및 시각화를 위한 핵심 라이브러리의 구조와 역할을 설명할 수 있다.
- Python 환경에서 데이터 분석에 필수적인 라이브러리를 임포트하고 기본 데이터를 가공 및 시각화할 수 있다.

## 사용 프로그램

- VS Code
- Jupyter Notebook

## 사용 라이브러리

- Pandas
- NumPy
- Matplotlib
- Seaborn

## 1. 실습 환경 준비

### 1.1 프로젝트 생성

```bash
uv init chapter01
```

### 1.2 패키지 설치

```bash
uv add numpy pandas matplotlib seaborn ipykernel
```

Windows에서는 보통 다음 방식으로 가상환경을 활성화한다.

```powershell
.venv\Scripts\activate
```

macOS/Linux에서는 다음 명령을 사용한다.

```bash
source .venv/bin/activate
```

Jupyter Notebook의 커널은 프로젝트의 `.venv` Python 환경을 선택한다.

## 2. 탐색적 데이터 분석(EDA)

**EDA(Exploratory Data Analysis)** 는 본격적인 분석이나 모델링 전에 데이터를 요약하고 시각화하여 구조와 특징을 파악하는 과정이다.

확인해야 할 대표 항목은 다음과 같다.

- 데이터 타입
- 결측치(Missing Value)
- 이상치(Outlier)
- 중복 데이터
- 분포
- 변수 간 관계

### 2.1 문자열로 저장된 숫자 처리

숫자에 `$`, `₩`, `,` 등의 문자가 포함되면 문자열로 인식될 수 있다.

```python
df['price'] = df['price'].str.replace('$', '', regex=False)
df['price'] = df['price'].str.replace(',', '', regex=False)
df['price'] = pd.to_numeric(df['price'])
```

분석 전에 `df.info()`로 데이터 타입을 확인하는 습관이 중요하다.

### 2.2 결측치 처리

- 숫자형: 평균(mean), 중앙값(median) 등을 사용
- 범주형: 최빈값(mode) 등을 사용
- 결측 비율이 매우 높거나 의미 없는 컬럼은 삭제를 검토

### 2.3 이상치 처리

다른 데이터와 비교해 지나치게 크거나 작은 값을 이상치라고 한다. Box Plot 등을 활용해 확인할 수 있다.

## 3. 기초 탐색 함수

### info()

```python
df.info()
```

행 개수, 컬럼, 데이터 타입, non-null 개수를 확인한다.

### describe()

```python
df.describe()
```

숫자형 컬럼의 평균, 표준편차, 최소값, 사분위수, 최대값 등을 확인한다.

### 결측치 개수

```python
df.isnull().sum()
```

## 4. Pandas Copy-on-Write와 안전한 수정

Pandas에서는 데이터 일부를 선택한 뒤 수정할 때 원본과 복사본 사이에서 문제가 발생할 수 있다.

가능하면 연속 대괄호 방식보다 `.loc[]` 또는 `.iloc[]`을 사용한다.

```python
df.loc[:, 'age'] = df['age'].fillna(df['age'].mean())
```

연속 대괄호 방식은 피한다.

```python
# 권장하지 않음
df['A']['B'] = value
```

## 5. 타이타닉 데이터 정제 예시

### 5.1 데이터 정보 확인

```python
df.info()
print('-' * 100)
df.describe()
```

### 5.2 결측치 확인

```python
df.isnull().sum()
```

### 5.3 숫자형 결측치 처리

```python
mean_age = df['age'].mean()
df.loc[:, 'age'] = df['age'].fillna(mean_age)
```

### 5.4 범주형 결측치 처리

```python
mode_embarked = df['embark_town'].mode()[0]
df.loc[:, 'embark_town'] = df['embark_town'].fillna(mode_embarked)

df.loc[:, 'embarked'] = df['embark_town'].map(lambda x: x[0].upper())
```

### 5.5 앞/뒤 값으로 결측치 채우기

```python
df.loc[:, 'deck'] = df['deck'].ffill()
df.loc[:, 'deck'] = df['deck'].bfill()
```

### 5.6 이상치 필터링

```python
df = df[df['fare'] < 300]
```

단, 실제 프로젝트에서는 단순히 임계값으로 제거하기 전에 해당 값이 오류인지, 실제 의미 있는 극단값인지 확인해야 한다.

## 6. 중복 데이터 처리

### 중복 개수 확인

```python
duplicate_count = df.duplicated().sum()
print(f'중복된 데이터 개수: {duplicate_count}개')
```

### 중복 행 전체 확인

```python
duplicated_rows = df[df.duplicated(keep=False)]
duplicated_rows
```

### 중복 제거 및 인덱스 초기화

```python
df = df.drop_duplicates().reset_index(drop=True)
```

## 7. 시각화

주요 그래프의 목적은 다음과 같다.

| 그래프 | 확인 목적 |
| --- | --- |
| 히스토그램 | 데이터 분포 |
| 박스 플롯 | 중앙값, 사분위수, 이상치 |
| 산점도 | 두 변수 간 관계 |

### 한글 폰트 설정

```python
import platform
import matplotlib.pyplot as plt

os_name = platform.system()
if os_name == 'Windows':
    plt.rcParams['font.family'] = 'Malgun Gothic'
elif os_name == 'Darwin':
    plt.rcParams['font.family'] = 'AppleGothic'
else:
    plt.rcParams['font.family'] = 'NanumGothic'

plt.rcParams['axes.unicode_minus'] = False
```

## 8. 타이타닉 분석에서 읽을 수 있는 것

- 나이 결측치를 평균으로 대체하면 평균값 부근에 데이터가 인위적으로 몰릴 수 있다.
- 1등석은 다른 등급보다 요금이 높고 분포도 넓다.
- 높은 요금과 생존 여부 사이에 연관성이 관찰될 수 있지만, 이것만으로 인과관계를 단정해서는 안 된다.

## 9. 개념 체크

### Q1

문자열로 잘못 인식된 숫자를 실제 숫자로 변환하는 Pandas 함수는?

**정답: `pd.to_numeric()`**

### Q2

범주형 데이터의 결측치를 채우는 대표적인 방법은?

**정답: 최빈값(mode)**

## 핵심 키워드

- EDA: 데이터를 요약하고 시각화하여 특징을 탐색하는 과정
- `info()`: 데이터 타입, 행/열, 결측 여부 확인
- `describe()`: 숫자형 데이터 기초 통계량 확인
- `to_numeric()`: 문자열 형태의 숫자를 숫자 타입으로 변환
- Missing Value: 결측치
- Mode: 최빈값
- Outlier: 이상치
- `.loc[]`: 명시적 위치 기반 데이터 선택/수정
- `duplicated()`: 중복 확인
- `drop_duplicates()`: 중복 제거

---

## 오늘의 한 줄 정리

**머신러닝은 데이터를 통해 규칙을 학습하는 기술이고, 좋은 모델을 만들기 위해서는 먼저 데이터를 제대로 이해하고 정제하는 EDA 과정이 필요하다.**
