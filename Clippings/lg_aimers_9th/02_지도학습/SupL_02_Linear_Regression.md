---
title: "Linear Regression"
series: 지도학습
lecture: 2
tags:
  - lg_aimers_9th
  - SupervisedLearning
  - 지도학습
  - LinearRegression
  - Overfitting
  - Regularization
aliases:
  - "지도학습 2강"
  - "Linear Regression"
created: 2026-06-23
related:
  - "[[SupL_01_Supervised_Learning_Overview]]"
  - "[[SupL_03_Gradient_Descent]]"
---

# Linear Regression

> [!abstract] 강의 개요
> [[SupL_01_Supervised_Learning_Overview|1강]] ← **지도학습 2강** → [[SupL_03_Gradient_Descent|3강]]
>
> 1강에서 본 단순 선형회귀를 **다차원**으로 확장하고, ==Normal Equation==으로 닫힌 해(closed-form solution)를 구한다. 이어서 feature를 추가할 때 발생하는 ==Overfitting==/Underfitting 문제를 Bias-Variance 관점에서 다루고, Train/Validation/Test 분할과 Regularization·Augmentation 같은 대응법을 정리한다.

> [!summary]- 핵심 요약 (클릭해서 펼치기)
> | 주제 | 핵심 |
> | ---- | ---- |
> | 다차원 선형회귀 | $g_\theta(x) = a_1x_1+a_2x_2+b$, loss는 여전히 quadratic |
> | Normal Equation | $\mathbf{a} = (X^TX)^{-1}X^TY$ — gradient = 0인 지점의 닫힌 해 |
> | Feature 추가 | 비선형 패턴도 feature 재정의로 선형회귀 틀 안에서 적합 가능 (e.g., 다항회귀) |
> | Overfitting | feature가 많을수록 표현력↑, 과적합 위험↑ — ==Bias-Variance Tradeoff== |
> | 데이터 분할 | Train(~80%) / Validation(~20%) / Test(별도) |
> | 대응법 | 데이터 추가, **Regularization**(L2), **Augmentation** |

## 목차

1. [[#1. 다차원으로의 확장]]
2. [[#2. Normal Equation — 닫힌 해 구하기]]
3. [[#3. Feature 재정의로 비선형 패턴 적합하기]]
4. [[#4. Overfitting과 Bias-Variance Tradeoff]]
5. [[#5. Train-Validation-Test 분할]]
6. [[#6. Overfitting 대응법]]
   - [[#6.1 Regularization]]
   - [[#6.2 Data Augmentation]]

---

## 1. 다차원으로의 확장

> [!note] (Height, Hand Size) → Weight
> 입력이 2차원으로 확장된 경우:
> $$x = (x_1, x_2),\quad x\in\mathcal{X}=\mathbb{R}^2,\ y\in\mathcal{Y}=\mathbb{R}$$
> $$\mathcal{G} = \{g_{a_1,a_2,b}(x) = a_1x_1 + a_2x_2 + b\}, \qquad \theta=(a_1,a_2,b)$$
>
> Loss는 여전히 **이차함수(quadratic)** 형태:
> $$L(a_1,a_2,b) = \frac{1}{3}\Big[C - 2a_1S_{x_1y} - 2a_2S_{x_2y} - 2bS_y + a_1^2S_{x_1x_1} + 2a_1a_2S_{x_1x_2} + a_2^2S_{x_2x_2} + 3b^2\Big]$$

> [!tip] 최소화 조건
> 이차함수이므로 ==Gradient = 0==인 지점이 최솟값:
> $$\nabla L(a_1,a_2,b) = \left(\frac{\partial L}{\partial a_1}, \frac{\partial L}{\partial a_2}, \frac{\partial L}{\partial b}\right) = \mathbf{0}$$
> $n+1$개의 변수에 대한 **선형 연립방정식**으로 풀 수 있다.

---

## 2. Normal Equation — 닫힌 해 구하기

> [!note] 행렬 표기
> $$X = \begin{bmatrix}x^{(1)}\\x^{(2)}\\\vdots\\x^{(n)}\end{bmatrix}\in\mathbb{R}^{n\times d}, \qquad Y = \begin{bmatrix}y^{(1)}\\y^{(2)}\\\vdots\\y^{(n)}\end{bmatrix}\in\mathbb{R}^n$$
>
> $$\mathcal{L}(\mathbf{a}) = \left\| \begin{bmatrix} \mathbf{a}^\top x^{(1)} - y^{(1)} \\ \vdots \\ \mathbf{a}^\top x^{(n)} - y^{(n)} \end{bmatrix}\right\|^2 = \|X\mathbf{a}-Y\|^2 = Y^TY - 2Y^TX\mathbf{a} + \mathbf{a}^TX^TX\mathbf{a}$$

> [!success] Normal Equation 유도
> Gradient를 0으로 설정:
> $$\frac{\partial \mathcal{L}(\mathbf{a})}{\partial \mathbf{a}} = -2X^TY + 2X^TX\mathbf{a} = 0$$
> $$\Rightarrow\ X^TX\mathbf{a} = X^TY \quad\Rightarrow\quad \boxed{\mathbf{a} = (X^TX)^{-1}X^TY}$$
>
> 이것이 선형회귀의 ==Normal Equation== — gradient descent 없이 **한 번의 행렬 연산**으로 최적해를 구할 수 있다.

---

## 3. Feature 재정의로 비선형 패턴 적합하기

> [!quote] "이차방정식을 적합하고 싶다면?"
> 데이터가 곡선 형태를 보일 때, **이것이 quadratic regression인가? → No.** 대신 데이터셋을 재정의(feature 변환)하면 동일한 선형회귀 틀로 풀 수 있다: 입력을 $x \to (x, x^2)$처럼 변환하고, 손실 함수는 동일한 MSE를 사용해 파라미터 "a"(새 feature의 계수)를 적합한다.

> [!tip] Feature를 더 추가할 수 있다
> 다차원 입력에 대해 다양한 feature(다항식 항, 교차항 등)를 추가할수록 모델은 더 표현력이 커지지만, ==overfitting==에 주의해야 한다. Feature는 데이터 검토(inspection)나 전문 지식(expertise)을 통해 선택할 수 있다.

---

## 4. Overfitting과 Bias-Variance Tradeoff

> [!warning] Underfitting vs Overfitting
> | | High Bias (Underfit) | Just Right | High Variance (Overfit) |
> | --- | --- | --- | --- |
> | 모델 | 너무 단순 | 적절 | 너무 복잡 |
> | 증상 | 패턴을 못 잡음 | 일반화 잘 됨 | 노이즈까지 암기 |

> [!note] 데이터가 많을수록 좋다
> 데이터가 많아지면 한두 개의 ==altered point==(이상치성 변형)에 덜 민감해져 더 안정적인 적합이 가능하다.

> [!tip] Overfitting을 어떻게 알아차리는가
> 고차원 데이터는 시각화가 어려우므로, **validation set**을 이용해 판단한다:
> - Train loss ≈ 0, Validation loss ≫ Train loss → **Overfitting 의심**
> - Train loss ≈ Validation loss → ==Generalization==이 잘 되고 있음

> [!example] 판단 기준
> - 사전 지식/이론에 기반 (==Occam's Razor==: 가장 적은 가정을 요구하는 설명이 보통 옳다)
> - 데이터 검토: training error가 낮은가?
> - Train error ≈ Validation error → Good
> - Train error ≪ Validation error → Overfit

---

## 5. Train-Validation-Test 분할

> [!note] 세 데이터셋의 역할
> | 구분 | 비율(예시) | 역할 |
> | ---- | ---------- | ---- |
> | **Train set** | 약 80% | 모델을 fit |
> | **Validation set** | 나머지 20% | 모델을 validate (하이퍼파라미터·모델 선택에 영향) |
> | **Test set** | 별도 데이터셋 | 모델을 test |

> [!warning] Test set은 학습 단계에서 미지(unknown)여야 한다
> 대회(competition) 상황을 생각해보면, test set은 흔히 학습 시점에 보이지 않는다. **Validation도 모델 선택 의사결정에 영향**을 주므로, 진짜 일반화 성능을 보려면 test set은 끝까지 분리해 두어야 한다.

---

## 6. Overfitting 대응법

> [!tip] Overfitting일 때 할 수 있는 것들
> - 더 많은 데이터 확보 (비용이 큼) — 생성모델로 샘플을 만드는 것도 가능하나 주의 필요
> - **Regularization**
> - **Augmentation** (데이터를 늘리는 효과)

### 6.1 Regularization

> [!note] L2 정규화
> 손실에 정규화 항(예: L2)을 추가해 과적합을 방지한다.
> - 정규화 강도가 **클수록** → 더 강하게 정규화 (단순한 모델로)
> - 정규화 강도가 **작을수록** → 덜 정규화 (복잡한 모델 허용)

### 6.2 Data Augmentation

> [!example] Augmentation 기법들
> "이동한(shifted) 강아지도 여전히 강아지다" — ==Translation invariant== 같은 직관을 이용해 데이터를 증강한다.
> - Flip, Enlarge, Rotate, Add noise, Color jitter 등

> [!warning] 데이터셋에 따라 다르다
> Augmentation은 데이터의 의미를 보존해야 한다. 예: 숫자 '2'를 좌우 반전(horizontal flip)하면 더 이상 '2'가 아니다 — **task에 적합한 augmentation을 신중히 선택**해야 한다.

> [!info] 데이터가 부족할 때
> Cross-Validation을 사용하면 적은 데이터로도 더 신뢰성 있는 모델 평가가 가능하다.

---

> [!success] 이번 강의 정리
> - **Normal Equation**으로 선형회귀의 닫힌 해 $\mathbf{a}=(X^TX)^{-1}X^TY$를 구할 수 있다
> - Feature 재정의로 비선형 패턴도 선형회귀 틀 안에서 다룰 수 있지만 **Overfitting vs Underfitting**의 trade-off가 생긴다
> - **Train vs Validation** 성능 차이로 과적합을 진단하고, **Regularization·Augmentation**으로 대응한다

---

%%
관련 노트:
- [[SupL_01_Supervised_Learning_Overview]] — 1강: 지도학습의 일반 틀과 선형회귀 도입
- [[SupL_03_Gradient_Descent]] — 3강: Normal Equation이 어려울 때의 대안, Gradient Descent
%%
