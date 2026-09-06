---
title: "Mathematics for ML"
series: Mathematics for ML
lecture: 1
instructor: Jinwoo Shin (KAIST AI)
tags:
  - lg_aimers_9th
  - MathematicsForML
  - LinearAlgebra
  - MatrixDecomposition
  - ConvexOptimization
  - PCA
  - SVD
aliases:
  - "Mathematics for ML"
  - "MathML"
created: 2026-06-23
---

# Mathematics for ML

> [!abstract] 강의 개요
> **Mathematics for ML** (단일 강의자료, 3개 세부 Lecture로 구성)
>
> ML의 수학적 기초 세 갈래 — **(1) 행렬 분해**(determinant/eigenvalue/Cholesky/EVD/SVD), **(2) Convex Optimization**(Gradient Descent/Lagrange Duality/KKT), **(3) PCA**(차원 축소) — 를 다룬다. 특히 PCA는 행렬 분해(SVD/EVD)와 최적화(Lagrange multiplier)가 어떻게 결합되어 하나의 알고리즘을 이루는지 보여주는 종합적인 사례다.

> [!summary]- 핵심 요약 (클릭해서 펼치기)
> | Lecture | 핵심 내용 |
> | ------- | --------- |
> | **1. Matrix Decompositions** | $\det(A)$·$\text{tr}(A)$로 행렬을 요약, ==Eigenvalue/Eigenvector==, Cholesky($A=LL^\top$), 대각화($A=PDP^{-1}$), ==SVD==($A=U\Sigma V^\top$) |
> | **2. Convex Optimization** | Gradient Descent의 변형들, Lagrange multiplier·duality, KKT 조건, LP/QP |
> | **3. PCA** | 분산을 최대화하는 저차원 투영 = 데이터 공분산 행렬의 top-M 고유벡터, SVD로 효율적 계산 |

## 목차

1. [[#1. Matrix Decompositions]]
   - [[#1.1 Determinant와 Trace]]
   - [[#1.2 Eigenvalue와 Eigenvector]]
   - [[#1.3 Cholesky Decomposition]]
   - [[#1.4 대각화 (Diagonalization)]]
   - [[#1.5 Singular Value Decomposition (SVD)]]
2. [[#2. Convex Optimization]]
   - [[#2.1 Gradient Descent 알고리즘들]]
   - [[#2.2 제약 최적화와 Lagrange Multiplier]]
   - [[#2.3 Convex Set과 Convex Function]]
   - [[#2.4 Convex Optimization, Strong Duality, KKT]]
3. [[#3. Principal Component Analysis (PCA)]]
   - [[#3.1 문제 설정]]
   - [[#3.2 Maximum Variance Perspective]]
   - [[#3.3 Eigenvector 계산과 Low-Rank Approximation]]
   - [[#3.4 고차원에서의 PCA]]

---

## 1. Matrix Decompositions

### 1.1 Determinant와 Trace

> [!note] Determinant (2×2, 3×3에서 일반화)
> $2\times2$ 행렬 $A$가 가역(invertible)이려면 $a_{11}a_{22}-a_{12}a_{21}\neq 0$ — 이를 $\det(A)$로 정의한다. 3×3 이상에서는 ==Laplace Expansion==으로 일반화:
> $$\det(A) = \sum_{k=1}^n (-1)^{k+j} a_{kj}\det(A_{k,j}) \quad (\text{column } j\text{에 대한 전개})$$
> ($A_{k,j}$: $k$행 $j$열을 제거한 부분행렬)
>
> > [!quote] 핵심 정리
> > $$\det(A)\neq 0 \iff \text{rk}(A)=n \iff A\text{는 가역}$$

> [!example] Determinant의 성질
> | 성질 | 내용 |
> | ---- | ---- |
> | 곱 | $\det(AB)=\det(A)\det(B)$ |
> | 전치 | $\det(A)=\det(A^\top)$ |
> | 역행렬 | $\det(A^{-1})=1/\det(A)$ |
> | 닮음행렬 | $A'=S^{-1}AS \Rightarrow \det(A)=\det(A')$ |
> | 삼각행렬 | $\det(T)=\prod_i T_{ii}$ |
> | 행/열 연산 | 한 행(열)에 다른 행(열)의 배수를 더해도 det 불변; 스칼라 곱은 $\det(\lambda A)=\lambda^n\det(A)$; 행/열 교환 시 부호 반전 |
>
> 이 성질들(특히 삼각행렬) 덕분에 **Gaussian elimination**으로 determinant를 계산할 수 있다.

> [!note] Trace
> $$\text{tr}(A) := \sum_{i=1}^n a_{ii}, \qquad \text{tr}(A+B)=\text{tr}(A)+\text{tr}(B), \quad \text{tr}(\alpha A)=\alpha\,\text{tr}(A), \quad \text{tr}(I_n)=n$$

### 1.2 Eigenvalue와 Eigenvector

> [!note] 정의
> 정방행렬 $A\in\mathbb{R}^{n\times n}$에 대해, $\lambda\in\mathbb{R}$이 **eigenvalue**, $\mathbf{x}\in\mathbb{R}^n\setminus\{0\}$이 그 **eigenvector**일 조건:
> $$A\mathbf{x} = \lambda\mathbf{x} \iff (A-\lambda I_n)\mathbf{x}=0 \text{가 } \mathbf{x}\neq 0\text{으로 풀림} \iff \det(A-\lambda I_n)=0$$

> [!example] 예시
> $A=\begin{pmatrix}4&2\\1&3\end{pmatrix}$의 특성방정식 $p_A(\lambda)=\lambda^2-7\lambda+10=0 \Rightarrow \lambda=2,5$.
> $\lambda=5$일 때 $E_5=\text{span}\begin{bmatrix}2\\1\end{bmatrix}$, $\lambda=2$일 때 $E_2=\text{span}\begin{bmatrix}1\\-1\end{bmatrix}$.
>
> > [!warning] Eigenvector는 유일하지 않다 (scale에 대해)

> [!success] 핵심 성질
> - $n$개의 distinct eigenvalue → eigenvector들은 선형독립이며 $\mathbb{R}^n$의 basis를 이룸 (역은 성립하지 않음)
> - $$\det(A) = \prod_{i=1}^n \lambda_i, \qquad \text{tr}(A) = \sum_{i=1}^n \lambda_i$$

### 1.3 Cholesky Decomposition

> [!quote] 직관
> 실수의 $9=3\times3$처럼, "행렬의 제곱근"에 해당하는 분해.

> [!note] 정리
> 대칭(symmetric)이고 양의 정부호(positive definite)인 $A$에 대해:
> $$A = LL^\top$$
> 여기서 $L$은 대각원소가 양수인 하삼각행렬(lower-triangular), 이 $L$은 **유일**하며 Cholesky factor라 부른다.

> [!example] 응용
> - 다변량 가우시안의 공분산 행렬 분해
> - 확률변수의 선형변환
> - 빠른 determinant 계산: $\det(A)=\det(L)^2=\prod_i l_{ii}^2$

### 1.4 대각화 (Diagonalization)

> [!note] Diagonal Matrix
> $$D=\text{diag}(d_1,\dots,d_n), \quad D^k=\text{diag}(d_1^k,\dots,d_n^k), \quad D^{-1}=\text{diag}(1/d_1,\dots,1/d_n), \quad \det(D)=\prod_i d_i$$

> [!note] 정의
> $A$가 **diagonalizable**: $\exists$ 가역 $P$ s.t. $D=P^{-1}AP$
> $A$가 **orthogonally diagonalizable**: $\exists$ 직교(orthogonal) $P$ s.t. $D=P^{-1}AP=P^\top AP$

> [!success] 대각화의 위력
> $$A^k = PD^kP^{-1}, \qquad \det(A)=\det(D)=\prod_i d_{ii}$$
> 거듭제곱·determinant 계산이 매우 쉬워진다.

> [!quote] Orthogonal Diagonalization ⟺ Symmetric
> $$A\text{는 orthogonally diagonalizable} \iff A\text{는 symmetric}$$
> **Spectral Theorem** (A가 symmetric일 때):
> (a) 모든 eigenvalue가 실수
> (b) 다른 eigenvalue에 대응하는 eigenvector들은 서로 직교
> (c) orthogonal eigenbasis가 존재
>
> → $P$의 column들이 $A$의 eigenvector들 ($AP=PD$, $P^\top=P^{-1}$).

### 1.5 Singular Value Decomposition (SVD)

> [!note] 배경
> 임의의 $A\in\mathbb{R}^{m\times n}$에 대해 $S:=A^\top A\in\mathbb{R}^{n\times n}$은 항상 **symmetric, positive semidefinite**이다 ($\mathbf{x}^\top S\mathbf{x}=\|A\mathbf{x}\|^2\ge 0$).

> [!success] SVD 정리
> rank $r$인 $A\in\mathbb{R}^{m\times n}$에 대해:
> $$A = U\Sigma V^\top$$
> $U\in\mathbb{R}^{m\times m}$, $V\in\mathbb{R}^{n\times n}$는 직교행렬, $\Sigma$는 $\Sigma_{ii}=\sigma_i\ge0$, 나머지는 0인 $m\times n$ 행렬 — **항상 존재하며 유일하게 결정**된다. $\sigma_i$를 ==singular value==, $u_i,v_j$를 left/right singular vector라 한다.

> [!example] EVD vs SVD
> | | EVD ($A=PDP^{-1}$) | SVD ($A=U\Sigma V^\top$) |
> | --- | --- | --- |
> | 존재 조건 | 정방행렬이고 eigenvector basis가 존재할 때 (e.g. symmetric) | **항상** 존재 |
> | $P$/$U,V$ | $P$는 일반적으로 비직교 (symmetric일 때만 직교) | $U,V$는 항상 직교 (rotation) |
> | 관계 | $A$가 symmetric이면 EVD = SVD (Spectral Theorem) | left/right singular vector는 각각 $AA^\top$, $A^\top A$의 eigenvector |

---

## 2. Convex Optimization

> [!quote] 핵심 메시지
> ML 모델 학습 = 좋은 파라미터를 찾는 것 = 어떤 최적화 문제의 (근사) 해를 찾는 것. 고등학교 수학의 $f'(x)=0$(정류점)이 출발점이며, ==Gradient==가 핵심 역할을 한다.

### 2.1 Gradient Descent 알고리즘들

> [!note] Unconstrained Optimization
> $$\min f(\mathbf{x}), \quad f:\mathbb{R}^n\to\mathbb{R} \qquad \mathbf{x}_{k+1} = \mathbf{x}_k + \gamma_k \mathbf{d}_k$$
> $\nabla f(\mathbf{x})\cdot \mathbf{d} < 0$인 방향 $\mathbf{d}$는 descent direction. ==Steepest gradient descent==: $\mathbf{d}_k=-\nabla f(\mathbf{x}_k)^\top$.

> [!example] Taxonomy
> | 분류 기준 | 종류 |
> | --------- | ---- |
> | 사용하는 데이터 양 | Batch(전체 $n$) / Mini-batch($k<n$) / Stochastic($k<n$, unbiased estimator) |
> | 업데이트 적응 방식 | Momentum, NAG, Adagrad, RMSProp, Adam 등 |

> [!note] SGD의 수학적 정의
> $\mathcal{L}(\theta)=\sum_{n=1}^N L_n(\theta)$일 때:
> $$\theta_{k+1} = \theta_k - \gamma_k\sum_{n=1}^N \nabla L_n(\theta_k)^\top \quad (\text{Batch})$$
> Mini-batch/SGD는 부분집합 $K$에 대해 $\sum_{n\in K}\nabla L_n(\theta_k)^\top$로 **noisy하지만 unbiased**한 근사를 사용: $\mathbb{E}\left[\sum_{n\in K}\nabla L_n(\theta_k)^\top\right] = \sum_{n=1}^N \nabla L_n(\theta_k)^\top$.

> [!tip] Momentum
> $$\mathbf{x}_{k+1} = \mathbf{x}_k - \gamma_k\nabla f(\mathbf{x}_k)^\top + \alpha\Delta\mathbf{x}_k, \qquad \Delta\mathbf{x}_k = \mathbf{x}_k-\mathbf{x}_{k-1}$$
> $\alpha\Delta\mathbf{x}_k$가 memory term — 과거 업데이트를 얼마나 "기억"할지를 조절해 진동(oscillation)을 완화한다.

### 2.2 제약 최적화와 Lagrange Multiplier

> [!note] 표준형 제약 최적화
> $$\text{minimize } f(\mathbf{x}) \quad \text{s.t.}\ g_i(\mathbf{x})\le 0\ (i=1,\dots,m), \quad h_j(\mathbf{x})=0\ (j=1,\dots,p)$$

> [!quote] Duality 발상
> 원 문제(primal)를 **다른 최적화 문제(dual)**로 bound하거나 풀 수 있다. **Lagrangian**:
> $$L(\mathbf{x},\lambda,\nu) = f(\mathbf{x}) + \sum_{i=1}^m \lambda_i g_i(\mathbf{x}) + \sum_{i=1}^p \nu_i h_i(\mathbf{x})$$
> **Lagrange dual function**: $D(\lambda,\nu)=\inf_{\mathbf{x}} L(\mathbf{x},\lambda,\nu)$

> [!success] Weak Duality (항상 성립)
> $$D(\lambda,\nu)\le p^\star \ \forall \lambda\succeq 0,\nu \qquad\Rightarrow\qquad d^\star \le p^\star$$
> ($p^\star$: primal 최적값, $d^\star$: **Lagrangian dual problem** $\max_{\lambda\succeq0} D(\lambda,\nu)$의 최적값. Dual 문제는 $D$가 $(\lambda,\nu)$에 대해 항상 concave하므로 **항상 convex 최적화**)

### 2.3 Convex Set과 Convex Function

> [!note] Convex Set
> $C$가 convex: $\forall x_1,x_2\in C,\ \theta\in[0,1]$에서 $\theta x_1+(1-\theta)x_2\in C$

> [!note] Convex Function
> $$f(\theta x+(1-\theta)y) \le \theta f(x)+(1-\theta)f(y)$$
> Affine 함수는 convex이자 concave. **Jensen's inequality**: $f(\mathbb{E}[X])\le \mathbb{E}[f(X)]$.

> [!example] 미분 가능 함수의 Convexity 조건
> | 차수 | 조건 |
> | ---- | ---- |
> | 1차 | $f(y)-f(x)\ge \nabla f(x)^\top(y-x)$ → local 정보(1차 Taylor)가 global 정보를 제공. $\nabla f(x)=0 \Rightarrow x$는 global minimizer |
> | 2차 | $\nabla^2 f(x)\succeq 0$ (양의 곡률) |

> [!example] 대표적인 Convex/Concave 함수
> $e^{ax}$(convex, $\forall a$), $x^a$($a\ge1$ or $a\le0$이면 convex), $\lvert x\rvert^p$($p\ge1$, convex), $\log x$(concave), $x\log x$(strictly convex), 모든 norm(convex), $\max\{x_1,\dots,x_n\}$(convex), $\log\sum_i e^{x_i}$(convex, log-sum-exp)

> [!tip] Convexity-Preserving Operations
> - 비음 가중합 $\sum_i w_if_i$ ($f_i$ convex, $w_i\ge0$) → convex
> - $g(x)=f(Ax+b)$는 $f$가 convex iff convex (affine 합성)
> - $\max\{f_1,f_2\}$는 $f_i$가 convex이면 convex
> - Pointwise supremum: $f(x,y)$가 $x$에 대해 convex이면 $g(x)=\sup_y f(x,y)$도 convex (Lagrange dual function이 concave인 이유와 동일한 원리)

### 2.4 Convex Optimization, Strong Duality, KKT

> [!quote] 핵심 통찰
> 쉽게 풀 수 있는 문제와 어려운 문제를 가르는 기준은 **'선형성'이 아니라 'Convexity'**다.

> [!success] Strong Duality
> $$d^\star = p^\star \quad (\text{optimal duality gap} = 0)$$
> **Convexity + constraint qualification(e.g., Slater's condition) ⟹ Strong Duality** — convex optimization이 "쉬운" 또 다른 이유.

> [!note] KKT (Karush-Kuhn-Tucker) Condition
> $$\nabla f(x^*) + \sum_i \lambda_i^* \nabla g_i(x^*) + \sum_j \nu_j^* \nabla h_j(x^*) = 0$$
> $$g_i(x^*)\le 0,\quad h_j(x^*)=0,\quad \lambda_i^*\succeq 0,\quad \lambda_i^* g_i(x^*)=0\ (\text{상보성, complementary slackness})$$
> Strong duality가 성립하는 모든 문제에서 KKT는 **필요조건**이며, convex 문제(+Slater 조건)에서는 **충분조건**이기도 하다.

> [!example] LP·QP — Lagrangian 적용 예
> **Linear Programming**: $\min_x \mathbf{c}^\top\mathbf{x}\ \text{s.t.}\ A\mathbf{x}\preceq\mathbf{b}$ → dual: $\max_\lambda -\mathbf{b}^\top\lambda\ \text{s.t.}\ \mathbf{c}+A^\top\lambda=0,\lambda\succeq0$
> **Quadratic Programming**: $\min_x \frac{1}{2}\mathbf{x}^\top Q\mathbf{x}+\mathbf{c}^\top\mathbf{x}\ \text{s.t.}\ A\mathbf{x}\preceq\mathbf{b}$ ($Q$: symmetric PD) → dual은 $Q^{-1}$을 포함하는 형태로 유도됨

---

## 3. Principal Component Analysis (PCA)

> [!quote] 동기
> 고차원 데이터는 분석·시각화가 어렵고 종종 중복(redundant) 정보를 포함한다. **압축된 표현이 항상 선호**된다 — PCA는 그 대표적인 방법.

### 3.1 문제 설정

> [!example] 직관: Housing Data
> 5차원(Size, 방 수, 욕실 수, 학교 수, 범죄율) → 2차원(Size feature, Location feature)으로 압축할 수 있다는 직관.

> [!note] PCA 알고리즘 5단계
> 1. **Centering**: 평균을 빼서 중심화
> 2. **Standardization**: 차원별 표준편차로 나눔
> 3. **Eigenvalue/vector**: 데이터 공분산 행렬의 상위 $M$개 eigenvalue/eigenvector 계산
> 4. **Projection**: eigenvector들이 정의하는 부분공간(principal subspace)에 투영
> 5. **Undo**: 표준화·중심화 역연산

> [!note] 표기
> $$X=[\mathbf{x}_1\ \cdots\ \mathbf{x}_N]\in\mathbb{R}^{D\times N} \text{(평균 0, 중심화됨)}, \qquad S=\frac{1}{N}XX^\top\in\mathbb{R}^{D\times D}$$
> Low-dim 표현(code): $\mathbf{z}_n = B^\top\mathbf{x}_n\in\mathbb{R}^M$, $B=(b_1,\dots,b_M)$의 열은 **orthonormal** ($b_i^\top b_j=\delta_{ij}$).
>
> > [!tip] Encoder-Decoder 관점
> > $B^\top$: encoder ($\mathbf{x}\to\mathbf{z}$), $B$: decoder ($\mathbf{z}\to\tilde{\mathbf{x}}$). (e.g., MNIST: $N=60{,}000$, $D=784$)

### 3.2 Maximum Variance Perspective

> [!quote] PCA의 목표
> 저차원 표현에서 **분산을 최대화**하는 orthonormal basis $B$를 찾는다. 결과적으로, 데이터 공분산 행렬 $S$의 상위 $M$개 eigenvalue에 대응하는 eigenvector가 바로 $b_1,\dots,b_M$이 된다.

> [!example] Step 1 — 첫 번째 주성분 $b_1$ 찾기
> 1차원 투영의 분산:
> $$V_1 = \frac{1}{N}\sum_n (b_1^\top \mathbf{x}_n)^2 = b_1^\top S b_1$$
> $$\max_{b_1} b_1^\top S b_1 \quad \text{s.t.}\ \|b_1\|^2=1$$
> Lagrange multiplier 방법으로 풀면:
> $$Sb_1 = \lambda_1 b_1,\quad b_1^\top b_1=1 \ \Rightarrow\ V_1 = \lambda_1$$
> **분산을 최대화하려면 가장 큰 eigenvalue를 선택** — 그 eigenvector가 첫 번째 주성분.

> [!example] Step $k$ — $k$번째 주성분 $b_k$ 찾기 (귀납법)
> $$\max_b b^\top S b \quad \text{s.t.}\ b^\top b=1,\ b^\top b_i=0\ (i=1,\dots,k-1)$$
> Lagrangian $L(b)=b^\top Sb - \lambda(b^\top b - 1)+\sum_i \eta_i b^\top b_i$의 1차 조건을 풀면 $\eta_j=0\ \forall j$가 도출되어 결국 $Sb_{k}=\lambda b_{k}$ — **$k$번째로 큰 eigenvalue에 대응하는 eigenvector**가 해가 된다 (Spectral theorem에 의해 $b_1,\dots,b_{k-1}$과 직교하도록 선택 가능).

### 3.3 Eigenvector 계산과 Low-Rank Approximation

> [!tip] 계산 방법 두 가지
> | 방법 | 절차 |
> | ---- | ---- |
> | **EVD** | $S$를 직접 고유분해 |
> | **==SVD==** | 데이터 행렬 $X=U\Sigma V^\top$ → $S=\frac{1}{N}XX^\top = \frac{1}{N}U\Sigma\Sigma^\top U^\top$ — $U$의 열이 $S$의 eigenvector, eigenvalue $\lambda_d = \sigma_d^2/N$ |

> [!success] PCA = Low-Rank Matrix Approximation
> 최적 rank-$M$ 근사 $\tilde X_M = \arg\min_{\text{rk}(A)=M}\|X-A\|^2$는, **Eckart-Young 정리**에 의해 SVD를 top-$M$ singular value에서 절단(truncate)한 것과 동일:
> $$\tilde X_M = U_M\Sigma_M V_M^\top = \sum_{i=1}^M \sigma_i u_i v_i^\top$$
> 즉 PCA는 분산 최대화 관점과 **재구성 오차(reconstruction error) 최소화** 관점이 동치임을 보여준다.

### 3.4 고차원에서의 PCA

> [!warning] $N \ll D$일 때의 문제
> $S=\frac{1}{N}XX^\top\in\mathbb{R}^{D\times D}$에서 $D$가 매우 클 때(예: $100\times100$ 이미지 → $D=10{,}000$), 중복 데이터가 없으면 $\text{rk}(S)=N$이고 $D-N+1$개의 eigenvalue가 0이다 — $D\times D$ 행렬 전체를 다룰 필요가 없다.

> [!success] Trick: $N\times N$ 행렬로 축소
> $Sb_m=\lambda_m b_m$에서 $\frac{1}{N}XX^\top b_m = \lambda_m b_m$이고, 양변에 $X^\top$를 곱하면:
> $$\frac{1}{N}\underbrace{X^\top X}_{N\times N}\underbrace{X^\top b_m}_{:=c_m} = \lambda_m X^\top b_m \iff \frac{1}{N}X^\top X\, c_m = \lambda_m c_m$$
> $\lambda_m$은 (훨씬 작은) $\frac{1}{N}X^\top X\in\mathbb{R}^{N\times N}$의 eigenvalue이고 $c_m=X^\top b_m$이 그 eigenvector — 이로부터 $X c_m$을 통해 $S$의 eigenvector를 복원할 수 있다.

---

> [!success] 전체 정리
> 이 강의자료는 ML의 세 가지 수학적 기둥을 보여준다: **행렬 분해**(SVD/EVD)는 데이터를 구조적으로 압축·분석하는 언어를, **Convex Optimization**(Lagrange duality/KKT)은 제약이 있는 문제를 푸는 일반적 틀을, **PCA**는 이 둘을 결합해 "분산 최대화 = eigenvalue 문제 = low-rank approximation"이라는 하나의 알고리즘으로 완성하는 사례를 제공한다.

---

%%
관련 노트:
- 본 강의자료는 LG Aimers 9기 단일 PDF로, 내부에 명확한 강 구분 마커가 없어 하나의 노트로 작성됨
%%
