---
title: "Classification"
series: 지도학습
lecture: 4
tags:
  - lg_aimers_9th
  - SupervisedLearning
  - 지도학습
  - Classification
  - Perceptron
  - SVM
  - HingeLoss
  - Kernel
aliases:
  - "지도학습 4강"
  - "Classification"
created: 2026-06-23
related:
  - "[[SupL_03_Gradient_Descent]]"
  - "[[SupL_05_Logistic_Regression]]"
---

# Classification

> [!abstract] 강의 개요
> [[SupL_03_Gradient_Descent|3강]] ← **지도학습 4강** → [[SupL_05_Logistic_Regression|5강]]
>
> 이진 분류(Binary Classification)를 선형 결정 경계 찾기 문제로 정의하고, **Perceptron → Linear Programming → Margin 최대화(SVM) → Soft-margin SVM(Hinge Loss) → Kernel**로 이어지는 자연스러운 발전 과정을 다룬다. 핵심 줄기는 "0-1 loss는 미분 불가능하다"는 문제를 어떻게 우회하는가이다.

> [!summary]- 핵심 요약 (클릭해서 펼치기)
> | 방법 | 핵심 아이디어 | 한계 |
> | ---- | -------------- | ---- |
> | **Perceptron** | 오분류 샘플 방향으로 가중치 업데이트 | 해가 없으면 멈추지 않음 |
> | **Linear Programming** | 제약(constraint) 충족 여부만 확인 | 해가 여러 개일 때 선택 기준 없음 |
> | **==SVM==** (Margin 최대화) | 가장 가까운 점까지의 거리(margin)를 최대화 | 선형 분리 불가능하면 infeasible |
> | **Soft-margin SVM** | slack variable로 오차 허용 | convex QP 필요 |
> | **Hinge Loss** | $\max(0, 1-y(\mathbf{a}^\top x+b))$ | — |
> | **Kernel** | feature를 확장해 비선형 경계 표현 | — |

## 목차

1. [[#1. Classification vs Regression]]
2. [[#2. Binary Classification의 Setup]]
3. [[#3. Perceptron Algorithm]]
4. [[#4. Linear Programming 관점]]
5. [[#5. Margin과 Support Vector Machine]]
6. [[#6. Soft-margin SVM과 Hinge Loss]]
7. [[#7. Kernel — 비선형 경계로 확장]]

---

## 1. Classification vs Regression

> [!note] 복습
> - **Classification**: 출력이 이산적(discrete, finite)
> - **Regression**: 출력이 연속적(continuous, real)

---

## 2. Binary Classification의 Setup

> [!note] 데이터와 함수 클래스
> $$(x^{(1)},y^{(1)}), \dots, (x^{(n)},y^{(n)}), \quad x^{(i)}=(x_1^{(i)},x_2^{(i)}),\ y^{(i)}\in\{-1,1\}$$
>
> **Linear Classifier**:
> $$\mathcal{G} = \{g_{a,b}(x) = \text{sign}(\mathbf{a}^\top x + b)\}$$
>
> **0-1 Loss**:
> $$\ell(g_{a,b}(x^{(i)}), y^{(i)}) = \mathbb{1}\big[g_{a,b}(x^{(i)}) \neq y^{(i)}\big]$$

> [!warning] 가정: 선형 분리 가능(Linearly Separable)
> Loss = 0인 완벽한 분류기가 존재한다고 가정한다. 하지만 ==0-1 loss는 미분 불가능==하기 때문에 gradient descent로 직접 최적화할 수 없다 — 이것이 이번 강의 전체를 관통하는 문제다.

---

## 3. Perceptron Algorithm

> [!note] Rosenblatt (1957)
> 가중치 $\mathbf{a}$, bias $b$를 초기화하고, 각 샘플에 대해 예측이 틀리면 그 샘플 방향으로 가중치를 업데이트한다.
> ```
> repeat
>     for each (x_i, y_i):
>         z_i = a·x_i + b
>         ŷ_i = sign(z_i)
>         if ŷ_i ≠ y_i:
>             a := a + η(y_i - ŷ_i)x_i
>             b := b + η(y_i - ŷ_i)
> until convergence
> ```

> [!success] 강점 / [!warning] 한계
> **강점**: 해가 존재하면 ==수렴이 보장==되고, 알고리즘이 매우 단순하다.
> **한계**: 해가 존재하지 않으면 **영원히 멈추지 않으며**, 그 사실을 알 방법이 없다.

---

## 4. Linear Programming 관점

> [!tip] Perceptron의 대안
> 목적함수 없이(Null objective), 제약 조건(constraint) 충족 여부만 확인하는 ==Linear Programming==으로 문제를 풀 수도 있다. 이 방식의 장점은 **문제가 infeasible(해가 없음)임을 명시적으로 알려준다**는 것 — Perceptron의 "영원히 멈추지 않는" 문제를 해결한다.

> [!warning] 새로운 질문
> 그런데 해가 여러 개 존재한다면(분리하는 직선이 무수히 많다면), **어떤 것을 선택해야 하는가?**

---

## 5. Margin과 Support Vector Machine

> [!note] Margin
> 결정 경계 $\mathbf{a}^\top \mathbf{x}+b=0$로부터 점 $\mathbf{x}_0$까지의 거리:
> $$d = \frac{|\mathbf{a}^\top \mathbf{x}_0 + b|}{\|\mathbf{a}\|}$$
>
> **Margin**은 가장 가까운 점까지의 거리이며, 이를 **최대화**하는 경계가 가장 ==Robust==하다는 직관이 SVM의 출발점이다.

> [!success] Support Vector Machine (SVM)
> $$\text{minimize}\quad \frac{1}{2}\|\mathbf{a}\|^2 \qquad \text{subject to}\quad y^{(i)}(\mathbf{a}\cdot \mathbf{x}^{(i)}+b)\ge 1 \quad \forall i$$
> 제약(margin ≥ 1)을 고정한 뒤 분모 $\|\mathbf{a}\|$를 최소화하는 형태로 변형해, margin을 최대화하는 것과 동치인 문제를 푼다.

> [!tip] 왜 풀 수 있는가
> SVM은 ==convex 문제==이며, 구체적으로는 **QCQP**(Quadratically Constrained Quadratic Program)다. 표준 solver로 풀 수 있고, 문제가 infeasible하면 그 사실을 알려준다.

---

## 6. Soft-margin SVM과 Hinge Loss

> [!warning] 해가 없을 때 (선형 분리 불가능)
> 기본 SVM 식은 오차를 전혀 허용하지 않으므로, 데이터가 선형 분리 불가능하면 infeasible하다는 답만 돌아온다.

> [!note] Soft-margin SVM — Slack Variable 도입
> 오차를 허용하기 위해 ==slack variable== $\xi_i$(penalty)를 추가:
> $$\text{minimize}\quad \frac{1}{2}\|\mathbf{a}\|^2 + C\sum_{i=1}^n \xi_i$$
> $$\text{subject to}\quad y_i(\mathbf{a}^\top \mathbf{x}_i + b) \ge 1-\xi_i,\ \ \xi_i\ge 0 \quad \forall i$$

> [!example] Hinge Loss로의 재해석
> $$\mathcal{L}(y_i, f(\mathbf{x}_i)) = \max\big(0,\ 1-y_i(\mathbf{a}^\top\mathbf{x}_i+b)\big)$$
> 이를 사용하면 soft-margin SVM의 목적함수는:
> $$\frac{1}{2}\|\mathbf{a}\|^2 + C\sum_{i=1}^n \mathcal{L}(y_i, f(\mathbf{x}_i))$$
>
> > [!tip] Regularization 강도 $C$의 역할
> > - **큰 $C$**: 오차(outlier)에 더 큰 페널티 → outlier에 민감
> > - **작은 $C$**: 일반적인(regular) 샘플에 집중 → margin을 더 중시

---

## 7. Kernel — 비선형 경계로 확장

> [!tip] Linear Regression과 동일한 직관
> 선형회귀에서 feature를 추가해 비선형 패턴을 적합했듯, 분류에서도 feature를 확장하면 비선형 결정 경계를 표현할 수 있다.

> [!example] Quadratic Kernel
> $$\tilde{x} = (x_1, x_2, x_1^2, x_2^2, x_1x_2)$$
> 확장된 feature space에서는 선형 경계가, 원래 공간에서는 비선형(예: 타원) 경계가 된다:
> $$x_1^2 - 2x_1x_2 + 2x_2^2 = 1$$

---

> [!success] 이번 강의 정리 (Summary: Classification)
> | 방법 | 핵심 한계/특징 |
> | ---- | -------------- |
> | **Perceptron** | 0-1 loss는 미분 불가능하므로 직접적인 gradient 최적화 대신 오분류 샘플 기반 업데이트 사용 |
> | **SVM** | 0-1 loss를 직접 쓰지 않고, **결정 경계 근처의 점들만** 고려해 margin을 최대화 (미분 가능한 형태로 재정의) |
> | **Soft-margin SVM** | 경계 근처의 점들 **+ violation을 일으키는 점들**까지 고려, convex optimization으로 해결 |

---

%%
관련 노트:
- [[SupL_03_Gradient_Descent]] — 3강: 미분 가능한 손실에 대한 일반적 최적화
- [[SupL_05_Logistic_Regression]] — 5강: 분류를 확률적으로 접근하는 대안 (Logistic Regression)
%%
