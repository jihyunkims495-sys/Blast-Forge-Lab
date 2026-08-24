# [특강] NumPy · Pandas · Matplotlib 학습정리

> 2026-08-24 특강 교안을 기준으로 먼저 구조화한 학습 노트입니다.  
> 수업 중 질의응답에서 실제로 헷갈린 부분과 이해가 바뀐 지점은 수업 종료 후 복습 단계에서 추가합니다.

## 1. 오늘 특강의 전체 흐름

이번 특강의 핵심은 **데이터를 배열로 다루고 → 표 형태로 정리하고 → 원하는 데이터만 추출·정제하고 → 그래프로 확인하는 전체 데이터 처리 흐름**을 익히는 것입니다.

```text
NumPy
배열 생성 · 슬라이싱 · shape 변경 · axis · broadcasting · 행렬 연산
        ↓
Pandas
Series · DataFrame · 탐색 · 인덱스 · 데이터 선택 · 결측치 처리 · groupby
        ↓
NumPy 변환
.to_numpy()
        ↓
Matplotlib
분포 · 관계 · 이상치 · 여러 그래프 시각화
```

---

# 2. NumPy 기초

## 2.1 NumPy는 무엇을 다루는가

NumPy의 핵심 자료구조는 `ndarray`입니다.

파이썬 리스트보다 수치 계산에 적합하고, 여러 행과 열을 가진 **N차원 배열**을 빠르게 처리할 수 있습니다.

```python
import numpy as np

matrix = np.array(
    [[10, 20, 30],
     [40, 50, 60],
     [70, 80, 90]],
    dtype=np.int64
)
```

### dtype

`dtype`은 배열 안의 값이 어떤 자료형으로 저장되는지 지정합니다.

```python
dtype=np.int64
dtype=np.float64
```

숫자 계산에서는 자료형을 통일하면 연산과 메모리 관리가 쉬워집니다.

---

## 2.2 2차원 배열 인덱싱과 슬라이싱

NumPy의 2차원 배열은 기본적으로 다음 구조로 접근합니다.

```python
배열[행, 열]
```

예시:

```python
matrix[0, 2]
```

- `0` → 0번째 행
- `2` → 2번째 열

즉 결과는 `30`입니다.

범위 선택:

```python
matrix[0:2, 1:3]
```

의미:

```text
0~1번 행
1~2번 열
```

전체 행에서 특정 열만 선택:

```python
matrix[:, 0]
```

여기서 `:`는 **전체 범위**를 의미합니다.

---

## 2.3 reshape와 flatten

### reshape()

원소 개수는 그대로 유지하고 배열의 모양(shape)만 바꿉니다.

```python
arr = np.arange(1, 13)
mat = arr.reshape(3, 4)
```

12개의 원소가:

```text
1차원 12개
→
3행 × 4열
```

로 변경됩니다.

```python
arr.reshape(3, -1)
```

`-1`은 **나머지 차원을 NumPy가 자동 계산하라**는 의미입니다.

### flatten()

다차원 배열을 다시 1차원으로 펼칩니다.

```python
flat = mat.flatten()
```

---

## 2.4 axis

`axis`는 **연산을 어느 방향으로 묶어서 수행할지**를 정합니다.

2차원 배열 기준:

```text
axis=0 → 행 방향으로 내려가며 계산 → 열별 결과
axis=1 → 열 방향으로 가며 계산 → 행별 결과
```

예시:

```python
matrix.sum(axis=0)
```

→ 각 열의 합

```python
matrix.sum(axis=1)
```

→ 각 행의 합

### 기억 포인트

`axis=0`을 단순히 "행"이라고 외우면 헷갈릴 수 있습니다.

**axis=0 방향을 없애며 계산하므로 결과는 열별 값이 남는다**고 이해하는 편이 안전합니다.

---

## 2.5 Broadcasting

브로드캐스팅은 크기가 다른 배열끼리 연산할 때 NumPy가 가능한 경우 작은 배열을 자동으로 확장해 계산하는 기능입니다.

예:

```python
mat + row_vec
```

행렬의 각 행에 같은 벡터가 반복 적용될 수 있습니다.

핵심은 실제로 배열을 여러 번 복사해서 만드는 것이 아니라 **연산 가능한 shape인지 판단하여 확장된 것처럼 계산한다**는 점입니다.

---

## 2.6 전치와 행렬곱

### 전치 `.T`

행과 열의 위치를 뒤집습니다.

```python
matrix.T
```

```text
3 × 4
→
4 × 3
```

### 행렬곱 `@`

```python
A @ B
```

일반적인 요소별 곱셈 `*`과 다릅니다.

- `*` → 같은 위치의 원소끼리 곱함
- `@` → 선형대수의 행렬곱

행렬곱에서는 **앞 행렬의 열 수와 뒤 행렬의 행 수가 같아야** 합니다.

---

# 3. Pandas 기초

## 3.1 Series와 DataFrame

### Series

Series는 **인덱스 + 한 줄의 데이터**로 구성된 1차원 구조입니다.

```python
pd.Series(...)
```

### DataFrame

DataFrame은 행과 열로 구성된 2차원 표 구조입니다.

```python
pd.DataFrame(...)
```

엑셀의 표와 비슷하지만, Python 코드로 검색·변경·집계·정제할 수 있다는 점이 핵심입니다.

---

## 3.2 DataFrame을 받으면 먼저 확인할 것

데이터 분석에서는 바로 계산하기보다 먼저 데이터 상태를 확인합니다.

### shape

```python
df.shape
```

```text
(행 개수, 열 개수)
```

### columns

```python
df.columns
```

열 이름 확인.

### dtypes

```python
df.dtypes
```

각 열의 자료형 확인.

### info()

```python
df.info()
```

- 행 개수
- 컬럼
- 결측치 여부
- dtype
- 메모리 사용량

등 데이터 구조를 종합적으로 확인합니다.

### describe()

```python
df.describe()
```

숫자형 컬럼의 기초 통계량을 확인합니다.

대표적으로:

```text
count
mean
std
min
25%
50%
75%
max
```

---

## 3.3 열 추가와 수정

Pandas에서는 기존 열을 이용해 새로운 열을 쉽게 만들 수 있습니다.

```python
df['보너스'] = df['급여'] * 0.1
```

이 연산은 각 행의 급여 값에 대해 한 번에 적용됩니다.

파이썬의 `for` 반복문을 직접 작성하지 않아도 컬럼 전체에 연산할 수 있다는 점이 중요합니다.

---

## 3.4 set_index와 reset_index

### set_index()

일반 열을 행의 인덱스로 사용할 수 있습니다.

```python
df.set_index('이름')
```

### reset_index()

인덱스를 다시 일반 열로 되돌리고 기본 숫자 인덱스를 생성합니다.

```python
df.reset_index()
```

---

## 3.5 Pandas의 Broadcasting

DataFrame과 Series를 연산하면 Pandas는 **인덱스와 컬럼 이름을 맞춰서 정렬한 뒤 연산**합니다.

NumPy가 주로 배열의 shape을 기준으로 동작한다면, Pandas는 **라벨(label)**까지 고려한다는 차이가 있습니다.

---

# 4. 원하는 데이터 정밀하게 조회하기

## 4.1 loc

`loc`는 **이름(label)** 기준입니다.

```python
df.loc[행_라벨, 열_라벨]
```

예:

```python
df.loc['김철수', '점수']
```

중요한 특징:

슬라이싱을 할 때 **끝 라벨을 포함합니다.**

---

## 4.2 iloc

`iloc`는 **위치(index number)** 기준입니다.

```python
df.iloc[행_위치, 열_위치]
```

예:

```python
df.iloc[0:2, 0:2]
```

파이썬 일반 슬라이싱과 같아서 끝 번호는 포함하지 않습니다.

### loc vs iloc

| 구분 | loc | iloc |
|---|---|---|
| 기준 | 라벨/이름 | 정수 위치 |
| 예 | `'Kim'`, `'score'` | `0`, `1`, `2` |
| 슬라이싱 끝값 | 포함 | 미포함 |

---

## 4.3 Boolean Indexing

조건식을 이용해 참인 행만 선택합니다.

```python
df[df['점수'] >= 80]
```

복합 조건에서는:

```python
(df['점수'] >= 80) & (df['출석률'] >= 90)
```

- `&` → AND
- `|` → OR

Pandas 조건식에서는 각 조건을 괄호로 묶는 습관이 중요합니다.

---

## 4.4 query()

조건식을 문자열 형태로 작성할 수 있습니다.

```python
df.query('점수 >= 80')
```

외부 Python 변수를 사용할 경우 `@`를 붙입니다.

```python
target_score = 80

df.query('점수 >= @target_score')
```

---

# 5. 결측치 처리

결측치는 값이 비어 있거나 정상적인 데이터로 해석할 수 없는 상태입니다.

예:

```text
NaN
<NA>
None
?
-
```

중요한 점은 **결측치를 무조건 0으로 채우거나 삭제하면 안 된다**는 것입니다.

왜 값이 없는지, 데이터의 성격이 무엇인지에 따라 처리 방법을 선택해야 합니다.

---

## 5.1 결측치 탐지

```python
df.isna()
```

각 값이 결측치인지 `True / False`로 확인합니다.

```python
df.isna().sum()
```

컬럼별 결측치 개수를 계산합니다.

---

## 5.2 삭제 dropna()

결측치가 포함된 행 또는 열을 제거합니다.

```python
df.dropna()
```

특정 열을 기준으로만 판단할 수도 있습니다.

```python
df.dropna(subset=['A'])
```

단점은 데이터 자체가 사라진다는 점입니다.

---

## 5.3 평균 또는 중앙값으로 대치

숫자형 데이터에서 결측치를 대표값으로 채울 수 있습니다.

```python
df['score'].fillna(df['score'].mean())
```

이상치가 많다면 평균보다 중앙값이 더 적합할 수 있습니다.

```python
df['score'].fillna(df['score'].median())
```

---

## 5.4 앞값/뒤값으로 채우기

시간 순서가 있는 데이터에서 자주 사용합니다.

```python
df.ffill()
```

→ 이전 유효값 사용

```python
df.bfill()
```

→ 다음 유효값 사용

---

## 5.5 선형 보간 interpolate()

앞뒤 값의 변화 흐름을 이용해 중간 값을 추정합니다.

```python
df.interpolate()
```

연속적인 수치 데이터나 시계열에서 사용할 수 있습니다.

---

## 5.6 이상 기호를 결측치로 바꾸고 숫자로 변환

실제 데이터에는 숫자 열에 `?`, `-` 같은 문자가 섞여 있을 수 있습니다.

이 경우 dtype이 `object`가 되어 숫자 계산이 어려워질 수 있습니다.

```python
df['score'] = pd.to_numeric(df['score'], errors='coerce')
```

`errors='coerce'`:

숫자로 변환할 수 없는 값을 `NaN`으로 바꿉니다.

주요 옵션:

```text
raise  → 변환 실패 시 에러 발생
coerce → 실패 값을 NaN으로 변환
ignore → 원래 값 유지
```

---

## 5.7 결측 여부 자체를 새로운 정보로 사용

어떤 데이터에서는 "값이 비어 있다는 사실" 자체가 의미가 있을 수 있습니다.

```python
df['소득_미응답'] = df['소득'].isna()
```

이렇게 결측 여부를 새로운 파생 변수로 만들 수 있습니다.

---

# 6. groupby와 NumPy 변환

## 6.1 groupby

범주별로 데이터를 묶어서 집계합니다.

```python
df.groupby('부서')['급여'].mean()
```

의미:

```text
부서별로 그룹 생성
→ 각 그룹의 급여 선택
→ 평균 계산
```

SQL의 `GROUP BY`와 연결되는 중요한 개념입니다.

---

## 6.2 to_numpy()

Pandas에서 전처리가 끝난 데이터를 NumPy 배열로 바꿀 수 있습니다.

```python
features = df[['age', 'income']].to_numpy()
```

Pandas는 라벨을 가진 표 데이터를 다루는 데 편리하고, NumPy는 수치 배열 연산에 적합합니다.

따라서 실제 데이터 파이프라인에서 두 라이브러리는 서로 연결해서 사용됩니다.

---

# 7. Matplotlib 기초

## 7.1 Figure와 Axes

Matplotlib 객체지향 방식의 핵심 구조는:

```python
fig, ax = plt.subplots()
```

입니다.

### Figure

전체 그림을 담는 도화지.

### Axes

실제 그래프가 그려지는 영역.

```text
Figure
└── Axes
    └── 실제 그래프
```

그래프의 제목이나 축 이름도 보통 `ax`를 통해 설정합니다.

```python
ax.set_title('Title')
ax.set_xlabel('X')
ax.set_ylabel('Y')
```

---

## 7.2 Scatter Plot

```python
ax.scatter(x, y)
```

두 연속형 변수 사이의 관계를 확인합니다.

예:

```text
광고비 ↔ 매출
키 ↔ 몸무게
공부시간 ↔ 점수
```

상관관계나 군집 패턴을 눈으로 확인할 때 사용합니다.

---

## 7.3 Bar Plot

```python
ax.bar(x, y)
```

범주별 크기를 비교할 때 적합합니다.

예:

```text
부서별 매출
제품별 판매량
지역별 회원 수
```

---

## 7.4 Histogram

```python
ax.hist(data)
```

숫자 데이터가 어느 구간에 얼마나 몰려 있는지 확인합니다.

즉 **데이터의 분포**를 보는 그래프입니다.

---

## 7.5 Box Plot

```python
ax.boxplot(data)
```

다음 정보를 빠르게 확인할 수 있습니다.

- 중앙값
- 데이터의 퍼짐
- 사분위 범위(IQR)
- 이상치
- 분포의 비대칭성

여러 집단의 박스플롯을 나란히 그리면 집단 간 분포를 비교하기 좋습니다.

---

## 7.6 Subplots

여러 그래프를 하나의 Figure에 배치할 수 있습니다.

```python
fig, axes = plt.subplots(2, 2)
```

```text
2행 × 2열
= 총 4개의 Axes
```

분석 결과를 한 화면에 비교하거나 간단한 분석 대시보드를 만들 때 유용합니다.

---

# 8. 오늘 특강에서 특히 연결해서 볼 개념

## NumPy 배열 ↔ Pandas DataFrame

```text
NumPy
숫자 배열 중심
shape / axis / broadcasting

Pandas
행·열 라벨이 있는 표 중심
index / column / loc / iloc / query
```

둘은 완전히 별개의 도구가 아니라 서로 연결됩니다.

---

## Python 기본 문법과의 연결

### 슬라이싱

기존 Python 리스트에서 배운:

```python
list[start:end]
```

개념이 NumPy와 Pandas에도 이어집니다.

### 조건식

기존 `if`에서 배운:

```python
score >= 80
```

같은 조건식이 Pandas에서는 여러 행에 한 번에 적용됩니다.

### 자료형

기존 `int`, `float`, `str` 개념이 NumPy/Pandas의 `dtype`과 연결됩니다.

---

# 9. 수업 중 질문이 나오면 집중해서 볼 포인트

수업 중 다음 항목은 코드 결과를 직접 따라가며 확인합니다.

1. `shape`가 현재 몇 행 × 몇 열인지
2. `axis=0`, `axis=1`에서 실제로 어떤 값이 묶이는지
3. `reshape()`에서 원소 개수가 왜 유지되어야 하는지
4. broadcasting에서 어떤 차원이 자동 확장되는지
5. Series와 DataFrame의 차이
6. `loc`와 `iloc`가 각각 무엇을 기준으로 찾는지
7. Boolean Indexing의 `&`, `|`와 기존 `and`, `or`의 차이
8. 결측치를 삭제·대치·보간 중 어떤 방식으로 처리해야 하는지
9. `groupby`의 실행 순서
10. Figure와 Axes의 관계

---

# 10. 수업 종료 후 복습 시 추가할 항목

- 오늘 실제로 새롭게 이해한 내용
- 수업 중 질문한 내용과 답
- 처음에는 헷갈렸지만 해결된 개념
- 아직 혼란스러운 개념
- 반복 취약점 후보
- 코드 실행 순서에서 막힌 부분
- 다음 복습 우선순위

> 이 문서는 현재 **교안 구조화 + 수업 중 질의응답 기준점** 상태입니다. 수업 종료 후 실제 학습 경험을 반영해 복습용 최종본으로 업데이트합니다.
