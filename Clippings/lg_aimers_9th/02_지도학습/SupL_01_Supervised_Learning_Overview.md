---
title: "Supervised Learning Overview"
series: 지도학습
lecture: 1
tags:
  - lg_aimers_9th
  - SupervisedLearning
  - 지도학습
  - MachineLearning
  - LinearRegression
aliases:
  - "지도학습 1강"
  - "Supervised Learning Overview"
created: 2026-06-23
related:
  - "[[SupL_02_Linear_Regression]]"
---

# Supervised Learning Overview

> [!abstract] 강의 개요
> **지도학습 1강** → [[SupL_02_Linear_Regression|2강]]
>
> 이미지 분류·번역·다음 단어 예측 같은 익숙한 문제들을 **지도학습(Supervised Learning)** 이라는 하나의 수학적 틀로 통합한다. "함수 근사"라는 관점에서 함수 클래스(function class)·손실 함수(loss function)를 정의하고, 가장 단순한 사례인 **선형 회귀**로 전체 흐름을 시연한다.

> [!summary]- 핵심 요약 (클릭해서 펼치기)
> | 개념 | 핵심 |
> | ---- | ---- |
> | 지도학습 | $(x,y)$ 쌍의 데이터로부터 $x\to y$ 매핑을 학습 |
> | Classification vs Regression | 출력이 이산(discrete)인가 연속(continuous)인가 |
> | 학습의 본질 | 참함수 $f^\star$를 함수 클래스 $\mathcal{G}$ 안에서 **근사** |
> | "잘 근사한다"의 정의 | 모든 입력이 아니라 **주어진 데이터셋**에서 유사한 함수값 |
> | Loss | pointwise loss(MSE, Cross-Entropy 등)의 합 |
> | 선형 회귀 | $\mathcal{G}$가 직선, loss가 MSE인 가장 단순한 사례 |

## 목차

1. [[#1. 지도학습이 푸는 문제들]]
2. [[#2. Rule-based에서 Machine Learning으로]]
3. [[#3. Supervised Learning의 두 유형]]
4. [[#4. 지도학습의 수학적 Setup]]
   - [[#4.1 함수 근사로서의 학습]]
   - [[#4.2 "잘 근사한다"를 정의하기 — Loss]]
5. [[#5. 사례 Linear Regression]]

---

## 1. 지도학습이 푸는 문제들

> [!example] 다양한 문제, 같은 구조
> | 문제 | 입력 $x$ | 출력 $y$ |
> | ---- | -------- | -------- |
> | Image Classification (CIFAR-10) | 이미지 | 클래스 레이블 |
> | Text Classification | 문장 | 감성(Positive 등) |
> | Next Word Prediction | "The cat sat on the ___" | 다음 단어 (mat 35%, table 30%, chair 32% …) |
> | Translation | 원문 | 번역문 |
> | Price Prediction | 매물 특성 | 가격 |

> [!quote] 공통점
> 이 모든 문제는 **데이터(x): 레이블/정답(y)** 쌍으로 정의되며, $x$로부터 $y$를 예측하는 함수를 찾는 문제로 환원된다.

---

## 2. Rule-based에서 Machine Learning으로

> [!warning] Rule-based Algorithm의 한계
> 전문가 지식·규칙 기반으로 직접 정의하려 하면:
> - "숫자 '0'을 정의하는 규칙은 무엇인가?"
> - "주가가 언제 오르는가?"
> 와 같은 질문에 명시적인 규칙으로 답하기 어렵고, **복잡한 task는 풀 수 없다**.

> [!success] Machine Learning의 전환
> 규칙을 직접 쓰는 대신, **데이터를 기반으로** 알고리즘이 스스로 규칙(패턴)을 찾아내게 한다.
>
> > [!quote] Arthur Samuel의 정의
> > *"Machine Learning is the field of study that gives computers the ability to learn without being explicitly programmed."*

---

## 3. Supervised Learning의 두 유형

> [!note] Classification vs Regression
> - **Classification**: 출력이 이산적(discrete, finite) — e.g., 이미지의 클래스 / (Translation)
> - **Regression**: 출력이 연속적(continuous, real) — e.g., 주택 가격
>
> (참고: ==Unsupervised Learning==은 레이블 없이 데이터 자체의 구조를 찾는 문제로, 지도학습과 대비된다.)

---

## 4. 지도학습의 수학적 Setup

### 4.1 함수 근사로서의 학습

> [!note] Setup
> - **참함수(True function)** $f^\star$: $f^\star(x^{(i)}) = y^{(i)}$를 만족하는 (알 수 없는) 함수
> - **목표**: $g(x) \approx f^\star(x)$를 만족하는 함수 $g$를 찾는 것
> - **함수 클래스(Function class)** $\mathcal{G}$: 탐색할 함수들의 집합 (e.g., 모든 직선, 모든 신경망 등)
> - **Goal**: $\mathcal{G}$ 안에서 $f^\star$를 잘 근사하는 $g_\theta$를 찾기
>
> $$g_\theta(x) \approx f^\star(x), \qquad g_\theta \in \mathcal{G}$$

> [!warning] "잘 근사한다"는 무엇을 의미하는가
> - **모든 입력 $x$에 대해** 유사한 함수값 → **[Infeasible]** (전체 입력 공간은 알 수 없음)
> $$g_\theta(x) \approx f^\star(x) \quad \text{(불가능)}$$
> - 대신, **주어진 데이터셋**에 대해서만 유사한 함수값을 요구
> $$g_\theta(x^{(i)}) \approx f^\star(x^{(i)}) = y^{(i)}$$

### 4.2 "잘 근사한다"를 정의하기 — Loss

> [!note] Pointwise Loss와 전체 Loss
> "유사한 함수값"을 정량적으로 측정하기 위해 **pointwise loss** $\ell$을 정의한다 (MSE, Cross-Entropy 등이 될 수 있음):
>
> $$\ell\big(g_\theta(x^{(i)}),\, y^{(i)}\big)$$
>
> 전체 데이터셋에 대한 **Loss**는 pointwise loss의 합:
>
> $$\mathcal{L}(\theta) = \sum_{i=1}^{n} \ell\big(g_\theta(x^{(i)}),\, y^{(i)}\big)$$

> [!success] 지도학습 절차 정리
> 1. 레이블 있는 데이터셋 $(x^{(1)},y^{(1)}), \dots, (x^{(n)},y^{(n)})$이 주어짐
> 2. 함수 클래스 $\mathcal{G}$ 설정
> 3. 손실 함수 $\ell$ 설정
> 4. $\mathcal{L}(\theta) = \sum_i \ell(g_\theta(x^{(i)}), y^{(i)})$를 **최소화**하는 $g_\theta \in \mathcal{G}$를 찾기

```mermaid
graph LR
    A["데이터셋 (x,y)"] --> B["함수 클래스 G 설정"]
    B --> C["손실 함수 ℓ 설정"]
    C --> D["L(θ) = Σ ℓ(g_θ(x_i), y_i) 최소화"]
    D --> E["학습된 모델 g_θ"]
```

---

## 5. 사례: Linear Regression

> [!example] Height vs. Weight 예시
> 키(height)와 체중(weight)이 양의 상관관계를 가질 때, **함수 클래스를 직선**으로 한정한 가장 단순한 지도학습 사례가 Linear Regression이다.

> [!note] 손실 함수: Mean-Squared Error (MSE)
> 3개의 데이터 포인트가 있다고 하면:
> $$L(a,b) = \frac{1}{3}\Big[(y^{(1)}-(ax^{(1)}+b))^2 + (y^{(2)}-(ax^{(2)}+b))^2 + (y^{(3)}-(ax^{(3)}+b))^2\Big]$$

> [!tip] 왜 절댓값이나 수직거리가 아니라 MSE인가
> 절댓값 차이나 점-직선 수직 거리도 합리적인 선택일 수 있지만, **MSE는 미분 가능(differentiable)하고 analytic solution이 존재**한다는 실용적 이점이 있다.

> [!example] Loss 전개와 정리
> $$L(a,b) = \frac{1}{3}\left[\sum_{i=1}^3 (y^{(i)})^2 - 2a\sum_{i=1}^3 y^{(i)}x^{(i)} - 2b\sum_{i=1}^3 y^{(i)} + a^2\sum_{i=1}^3 (x^{(i)})^2 + 2ab\sum_{i=1}^3 x^{(i)} + 3b^2\right]$$
>
> 충분 통계량($C, S_{xy}, S_y, S_{xx}, S_x$)으로 정리하면:
> $$L(a,b) = \frac{1}{3}\Big[C - 2aS_{xy} - 2bS_y + a^2 S_{xx} + 2abS_x + 3b^2\Big]$$

> [!success] 이번 강의 정리
> 지도학습은 (1) 레이블 있는 데이터셋, (2) 함수 클래스 $\mathcal{G}$, (3) 손실 함수를 정해두고, 손실을 최소화하는 $g_\theta$를 찾는 일반적인 틀이다. **Linear Regression**은 이 틀의 가장 단순한 인스턴스이며, 다음 강의에서 이 손실을 실제로 어떻게 최소화하는지(closed-form solution) 이어서 다룬다.

---

%%
관련 노트:
- [[SupL_02_Linear_Regression]] — 2강: Linear Regression의 해를 구하는 방법
%%
