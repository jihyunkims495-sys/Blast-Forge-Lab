# [MACHINE LEARNING] PyTorch·DNN·역전파·임베딩·RNN·LSTM 예습 정리

> **예습 목표: 아침 10분 안에 4장 전체 흐름을 잡는다.**  
> 코드 세부 문법보다 **신경망이 왜 깊어지는지 → 어떻게 오차를 역전파하는지 → PyTorch가 무엇을 자동화하는지 → 순서가 있는 데이터는 왜 RNN/LSTM으로 처리하는지**를 이해하는 것이 우선이다.

---

# 🚨 이것만 알고 강의 들어가기

## 핵심 5줄 요약

1. **DNN은 입력층과 출력층 사이에 여러 은닉층을 두고, 비선형 활성화 함수를 사용해 복잡한 패턴을 학습하는 신경망**이다.
2. 신경망 학습은 `Forward → Loss → Backpropagation → Optimizer Step`을 반복하는 과정이다.
3. **Backpropagation은 기울기를 계산하고, Optimizer는 그 기울기를 이용해 실제 가중치를 업데이트한다.**
4. 자연어처럼 순서가 중요한 데이터에서는 **Embedding으로 단어를 밀집 벡터로 바꾸고, RNN/LSTM으로 앞선 정보의 맥락을 이어간다.**
5. PyTorch에서는 `nn.Module`, `DataLoader`, `loss.backward()`, `optimizer.step()`, `model.train() / eval()` 흐름을 이해하는 것이 핵심이다.

### 중요도

- 🔥🔥🔥 **Forward → Loss → Backward → Update**
- 🔥🔥🔥 **은닉층 + 비선형 활성화 함수가 필요한 이유**
- 🔥🔥🔥 **ReLU / CrossEntropyLoss / Adam**
- 🔥🔥🔥 **model.train() vs model.eval()**
- 🔥🔥🔥 **Embedding → RNN/LSTM → 마지막 은닉 상태 → 분류**
- 🔥🔥 **Dropout / Early Stopping / Mini-batch**
- 🔥🔥 **Vanishing Gradient / LSTM Gate**

---

# 🗺️ 4장 전체 학습 구조

```text
PyTorch 딥러닝
├─ DNN → Linear → Hidden Layer → ReLU → Logits
├─ 학습 루프 → Forward → Loss → Backward → Optimizer Step
├─ 일반화 → Dropout / Early Stopping / Train·Valid·Test
└─ Sequence → Embedding → RNN → LSTM → 분류
```

# 🥇 핵심 개념

## 은닉층과 DNN

선형 변환만 사용하면 복잡한 경계를 표현하기 어렵다. 은닉층에서 Feature를 여러 번 변환하고 ReLU 같은 비선형 활성화 함수를 넣어 복잡한 표현을 학습한다.

```text
입력 → Linear → ReLU → Hidden → Linear → 출력
```

## Fashion MNIST와 Flatten

```text
28 × 28 이미지 → Flatten → 784 → Linear(784→128) → ReLU → Dropout → Linear(128→10)
```

Flatten은 정보를 학습하는 레이어가 아니라 shape을 바꾸는 레이어다.

## Parameter

**Parameter = Weight + Bias.** 신경망이 학습한다는 것은 내부 Weight와 Bias를 계속 조정한다는 뜻이다.

## 신경망 학습 흐름

```text
optimizer.zero_grad()
→ Forward
→ Loss
→ Backpropagation
→ optimizer.step()
```

- Backpropagation: 각 파라미터에 대한 Gradient 계산
- Optimizer: Gradient를 이용해 실제 Weight 수정
- 한 줄 구분: **Backward = 방향 계산 / Optimizer = 실제 이동**

## ReLU

```text
ReLU(x) = max(0, x)
x < 0 → 0
x > 0 → x
```

은닉층에서 비선형성을 넣는 데 자주 사용한다.

## Sigmoid / Softmax

```text
Hidden Layer → ReLU 자주 사용
Binary Output → Sigmoid 개념
Multiclass Output → Softmax 개념
```

PyTorch의 `CrossEntropyLoss`는 Logit을 직접 받으므로 학습 시 모델 마지막에 Softmax를 직접 넣지 않는 경우가 일반적이다.

## Mini-batch / DataLoader

전체 데이터를 작은 묶음으로 나눠 학습한다.

```python
DataLoader(dataset, batch_size=32, shuffle=True)
```

메모리를 절약하고 GPU 병렬 연산을 활용하며, 한 샘플씩 학습하는 것보다 안정적으로 학습할 수 있다.

## Train / Eval

```text
model.train() = 학습 모드, Dropout 활성화
model.eval() = 평가 모드, Dropout 비활성화
no_grad() = Gradient 기록 끄기
```

## Overfitting / Dropout / Early Stopping

```text
Train Loss ↓
Valid Loss ↑
→ Overfitting
```

Dropout은 훈련 중 일부 뉴런 출력을 랜덤하게 0으로 만들어 특정 뉴런 조합에 과도하게 의존하는 것을 줄인다. Early Stopping은 Validation 성능이 개선되지 않으면 학습을 중단한다.

---

# 🥇 Embedding → RNN → LSTM

## Embedding

One-Hot은 차원이 크고 단어 관계를 표현하기 어렵다. Embedding은 단어 인덱스를 저차원의 학습 가능한 실수 벡터로 매핑한다.

```text
One-Hot: [0,0,0,1,0,...]
Embedding: [0.18, -0.42, 0.91, ...]
```

Embedding 내부의 Weight Table 역시 Backpropagation으로 학습된다.

## RNN

RNN은 **순서가 중요한 데이터**를 처리한다.

```text
x1 + h0 → h1
x2 + h1 → h2
x3 + h2 → h3
```

Hidden State는 지금까지 본 시퀀스 정보를 압축해 다음 시점으로 넘기는 기억 벡터다.

## Vanilla RNN의 문제

시퀀스가 길어지면 시간 방향으로 역전파가 길어져 Vanishing Gradient / Exploding Gradient 문제가 발생할 수 있다.

## LSTM

기본 RNN의 장기 의존성 문제를 완화하기 위해 **Cell State와 Gate**를 도입한다.

```text
Forget Gate = 무엇을 버릴지
Input Gate = 무엇을 새로 저장할지
Output Gate = 무엇을 밖으로 보낼지
```

**LSTM = 기억 흐름을 Gate로 제어하는 RNN 개선 구조.**

---

# ⚠️ 헷갈리기 쉬운 구분

```text
Backpropagation ≠ Weight Update
Backpropagation = Gradient 계산
Optimizer = Weight Update
```

```text
model.eval() ≠ no_grad()
model.eval() = 모델 동작 모드 변경
no_grad() = Gradient 추적 비활성화
```

```text
Dropout = 뉴런 삭제가 아님
훈련 중 일부 출력을 일시적으로 0으로 만듦
```

```text
DNN = 일반적인 깊은 신경망
CNN = 이미지의 공간 관계 활용
RNN = 순서와 이전 정보 활용
```

---

# 🔗 이후 학습과 연결

```text
DNN
→ Backpropagation
→ Optimizer
→ Deep Learning
→ RNN / LSTM
→ Attention
→ Transformer
→ LLM
```

이번 장은 이후 LLM을 이해하기 위한 기반이다.

---

# ⏱️ 아침 10분 예습 코스

1. DNN: `Input → Linear → ReLU → Hidden → Linear → Logits`
2. 학습: `zero_grad → forward → loss → backward → optimizer.step`
3. 평가: `train / eval / no_grad` 구분
4. 과적합: `Dropout / Early Stopping`
5. 자연어: `Token ID → Embedding → RNN → Hidden State`
6. LSTM: `RNN 장기 기억 한계 → Cell State + Gate`

# ✅ 예습 완료 기준

> **“딥러닝 신경망은 Linear Layer 사이에 ReLU 같은 비선형 활성화 함수를 넣어 복잡한 패턴을 학습한다. PyTorch의 학습은 `zero_grad → forward → loss → backward → optimizer.step` 순서로 이루어지며, 역전파는 기울기를 계산하고 옵티마이저는 실제 가중치를 수정한다. 자연어처럼 순서가 중요한 데이터는 단어를 Embedding으로 밀집 벡터화한 뒤 RNN이나 LSTM으로 이전 정보를 Hidden State에 이어가며 처리한다.”**
