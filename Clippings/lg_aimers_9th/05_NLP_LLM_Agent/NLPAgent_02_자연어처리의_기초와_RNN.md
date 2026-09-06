---
title: "자연어처리의 기초와 RNN"
series: 딥러닝 자연어처리 기초와 LLM 에이전트
lecture: 2
instructor: 이환희 (중앙대학교 AI학과)
tags:
  - lg_aimers_9th
  - NLP
  - Tokenization
  - WordEmbedding
  - Word2Vec
  - LanguageModel
  - RNN
  - LSTM
aliases:
  - "NLPAgent 2강"
  - "자연어처리의 기초와 RNN"
created: 2026-06-23
related:
  - "[[NLPAgent_01_AI의_첫걸음_머신러닝과_딥러닝의_기초]]"
  - "[[NLPAgent_03_트랜스포머와_어텐션_메커니즘]]"
---

# 자연어처리의 기초와 RNN

> [!abstract] 강의 개요
> [[NLPAgent_01_AI의_첫걸음_머신러닝과_딥러닝의_기초|1강]] ← **NLPAgent 2강** → [[NLPAgent_03_트랜스포머와_어텐션_메커니즘|3강]]
>
> NLP 파이프라인의 세 단계(Preprocessing → Embedding → Modeling)를 따라가며, ==Tokenization==·==Word Embedding==(Word2Vec)·==Language Model==의 개념을 차례로 다진다. 가변 길이 시퀀스를 처리하기 위한 ==RNN==과, RNN의 한계(Vanishing Gradient)를 보완하는 ==LSTM==까지 — 다음 강의의 Transformer를 위한 토대를 마련한다.

> [!summary]- 핵심 요약 (클릭해서 펼치기)
> | 단계 | 핵심 |
> | ---- | ---- |
> | **Tokenization** | 텍스트를 토큰 단위로 분리, Vocab 크기의 trade-off(OOV vs 연산량) → BPE로 해결 |
> | **Word Embedding** | One-hot(BoW) → ==Word2Vec==(CBOW/Skip-gram)로 밀집·의미 보존 벡터 학습 |
> | **Language Model** | 단어 시퀀스의 확률분포 $P(w_1,\dots,w_T)$를 학습 |
> | **RNN** | 가변 길이 입력 처리, 매 step 동일 가중치 적용, BPTT로 학습 |
> | **한계** | Vanishing Gradient — 먼 과거 정보를 기억하기 어려움 |
> | **LSTM** | Input/Forget/Output 3개 게이트로 장기 의존성 보존 |

## 목차

1. [[#1. Natural Language Processing 개관]]
2. [[#2. Tokenization]]
3. [[#3. Word Embedding]]
   - [[#3.1 One-hot Encoding과 Bag-of-Words]]
   - [[#3.2 Word2Vec — CBOW와 Skip-gram]]
4. [[#4. Language Model]]
5. [[#5. Recurrent Neural Network (RNN)]]
   - [[#5.1 RNN의 구조와 장단점]]
   - [[#5.2 RNN 학습 — BPTT]]
   - [[#5.3 Vanishing Gradient와 LSTM]]

---

## 1. Natural Language Processing 개관

> [!note] NLP = NLU + NLG
> - **NLU (Natural Language Understanding)**: 텍스트를 이해
> - **NLG (Natural Language Generation)**: 텍스트를 생성
> - 대표 task: 기계번역, 요약, 대화 시스템(Dialog System), 스토리 생성

> [!note] NLP 시스템 구축 파이프라인
> $$\text{Preprocessing(Tokenization)} \to \text{Embedding} \to \text{Modeling}$$
> 예: `"I loved the movie"` → 토큰 `["I","loved","the","movie"]` → $N\times D$ 벡터($N$=단어 수, $D$=차원) → `"Positive"`

---

## 2. Tokenization

> [!note] Vocab Size의 Trade-off
> | 선택 | 문제점 |
> | ---- | ------ |
> | Vocab이 너무 작음 (e.g., word-level) | ==Out-of-Vocabulary(OOV)== — 사전에 없는 단어 처리 불가 |
> | Vocab이 너무 큼 (e.g., character-level 반대 극단) | 연산량 증가, sparsity 문제 |

> [!tip] 해결책: Byte Pair Encoding (BPE)
> Word-level과 Character-level의 중간 지점 — 자주 등장하는 문자열 조합을 점진적으로 병합해 subword 단위 vocab을 구성 (3주차에서 자세히 다룸).

---

## 3. Word Embedding

> [!note] 정의
> 단어를 실수 벡터로 매핑하는 표현 방법.

### 3.1 One-hot Encoding과 Bag-of-Words

> [!warning] Bag-of-Words(BoW)의 한계
> 텍스트를 단어들의 가방(bag)으로 표현 (e.g., one-hot encoding). 단어 간 **순서·의미적 유사도를 전혀 반영하지 못함** — "dog"와 "cat"이 의미적으로 가까워도 벡터 공간에서는 전혀 가깝지 않음.

### 3.2 Word2Vec — CBOW와 Skip-gram

> [!success] Word2Vec (Mikolov, 2013)
> 비슷한 context를 가진 단어들이 벡터 공간에서 **서로 가깝게** embedding되도록 학습하는 대표적 기법.

> [!example] 두 가지 목적함수
> | 모델 | 목표 | 손실 |
> | ---- | ---- | ---- |
> | **CBOW** (Continuous Bag-of-Words) | context로부터 center word 예측 | $E = -\log p(w_t \mid w_{t-c},\dots,w_{t+c})$ |
> | **Skip-gram** | center word로부터 context word 예측 | $E = -\log p(w_{t-c},\dots,w_{t+c} \mid w_t)$ |

> [!note] Skip-gram 구조
> $$h = W^\top x, \qquad u = W'^\top h, \qquad y_j = \frac{e^{u_j}}{\sum_{j'=1}^V e^{u_{j'}}}$$
> $y_j = p(w_j\mid w_i)$ — 입력 $w_i$가 주어졌을 때 $w_j$가 context word일 확률. **Hidden layer의 weight matrix $W$의 각 행이 바로 word vector**가 된다 (word vector look-up table).

---

## 4. Language Model

> [!note] 정의
> 문장·단어 시퀀스의 **확률분포를 학습**한 모델 — 대량의 텍스트로부터 문장의 패턴을 학습해 다음 단어를 예측하거나 새 문장을 생성.

> [!example] 어순과 단어선택을 모두 반영
> $$P(\text{the cat is small}) > P(\text{small the is cat}) \qquad P(\text{walking home after school}) > P(\text{walking house after school})$$

> [!success] Chain Rule로 시퀀스 확률 계산
> $$P(w_1,\dots,w_T) = P(w_1)P(w_2\mid w_1)P(w_3\mid w_1,w_2)\cdots P(w_n\mid w_1,\dots,w_{n-1})$$

> [!warning] Fixed-window Language Model의 한계
> 고정된 개수의 이전 단어만 고려하는 모델은 한계가 명확 — **"임의의 길이의 입력을 처리할 수 있는 신경망 구조가 필요하다"**는 것이 RNN 도입의 동기.

---

## 5. Recurrent Neural Network (RNN)

### 5.1 RNN의 구조와 장단점

> [!note] RNN이 시퀀스에 자연스러운 이유
> - 이산적인 시간(time step)에 따라 입력을 순서대로 처리
> - hidden state에 정보를 오래 "기억"
> - **매 시간 단계에서 동일한 weight를 반복 적용** — 한 hidden layer를 가진 매우 깊은 net과 동등하지만, 가중치 공유와 매 스텝 입력이라는 차이가 있음

> [!example] 장단점
> | 장점 | 단점 |
> | ---- | ---- |
> | 임의 길이 입력 처리 가능 | 순환 계산이라 느림 |
> | step $t$의 계산이 여러 단계 전 정보 활용 가능 | 실제로는 먼 과거 정보에 접근하기 어려움 |
> | 입력이 길어져도 모델 크기 불변 | — |
> | 매 시점 동일 weight → 처리의 대칭성 | — |

### 5.2 RNN 학습 — BPTT

> [!note] 학습 절차
> 1. 큰 텍스트 코퍼스(단어 시퀀스)를 확보
> 2. RNN-LM에 입력해 매 step $t$의 출력 분포 계산 — 지금까지의 단어들이 주어졌을 때 다음 단어의 확률분포 예측
> 3. **Cross-entropy loss**: 예측 분포와 실제 다음 단어(one-hot)의 차이
> 4. 전체 학습셋에 대한 평균으로 overall loss 계산

> [!tip] Teacher Forcing
> 학습 시, 모델이 이전 step에서 잘못 예측했더라도 **실제 정답을 다음 입력으로 사용**하는 기법 — 학습을 안정화.

> [!warning] 전체 corpus에 대한 동시 계산은 너무 비싸다
> 실제로는 ==Stochastic Gradient Descent==처럼 문장(또는 batch) 단위로 loss·gradient를 계산하고 업데이트를 반복한다.

> [!note] Backpropagation Through Time (BPTT)
> $$\frac{\partial J^{(t)}(\theta)}{\partial W_h} = \sum_{i=1}^t \frac{\partial J^{(t)}(\theta)}{\partial W_h}\Big|_{(i)}$$
> 반복되는(shared) weight matrix에 대한 gradient는 **그 weight가 사용된 모든 시점에서의 gradient의 합**이다 — RNN을 시간축으로 "풀어서(unroll)" backpropagation을 적용.

> [!example] RNN으로 텍스트 생성 ("Generating roll-outs")
> 매 step 샘플링된 출력이 다음 step의 입력이 되는 방식으로 반복 샘플링해 텍스트를 생성할 수 있다.

### 5.3 Vanishing Gradient와 LSTM

> [!warning] Vanishing Gradient 문제
> 기본 RNN에서는 시간이 지날수록 초기 입력의 영향력이 감소·소멸한다 — 즉, 멀리 떨어진 정보를 “잊어버린다”.

> [!success] LSTM (Long Short-Term Memory)
> Gradient 정보를 더 잘 보존 — **3개의 게이트**로 구성된 cell이 정보를 오래 저장·접근:
> | Gate | 역할 |
> | ---- | ---- |
> | **Input gate** | 입력이 cell에 미치는 영향 조절 |
> | **Forget gate** | cell이 시간에 따라 자신에게 미치는 영향(기억 유지 정도) 조절 |
> | **Output gate** | cell이 출력에 미치는 영향 조절 |

> [!example] RNN을 이용한 문장 인코딩
> 감성 분류(sentiment classification) 등에서, RNN의 최종(또는 중간) hidden state를 문장 전체의 표현으로 사용.

---

> [!success] 이번 강의 정리
> NLP는 텍스트 전처리(Tokenization) → 수치 벡터 표현(Word Embedding) → 모델링(Language Model)의 파이프라인을 따른다. **Word2Vec**은 의미적으로 가까운 단어를 벡터 공간에서도 가깝게 배치하며, **Language Model**은 단어 시퀀스의 확률을 체인룰로 분해해 학습한다. **RNN**은 가변 길이 시퀀스를 자연스럽게 처리하지만 **Vanishing Gradient**로 장기 의존성 학습에 한계가 있고, **LSTM**의 게이트 구조가 이를 보완한다.

---

%%
관련 노트:
- [[NLPAgent_01_AI의_첫걸음_머신러닝과_딥러닝의_기초]] — 1강: 신경망·Backpropagation 기초
- [[NLPAgent_03_트랜스포머와_어텐션_메커니즘]] — 3강: RNN의 한계를 Attention/Transformer로 극복
%%
