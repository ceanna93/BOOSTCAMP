# Ontology-based DST models
## 1. Ontology
### 1.1 Classification based DST Recap
Set(S^j)가 Ontology

**Ontology**: 각 Slot j가 가질 수 있는 Value의 후보군을 정의해둔 정보.
모든 Value는 이 안에서만 등장한다고 가정.

일종의 Prior Knowledge로 활용할 수 있다.

Value에 대한 확률적인 표현이 가능.

#### 한계점
- value의 후보군이 많아질수록 더 많은 value를 비교가 필요해 계산 비용이 증가. 특히 Ontogoly가 커졌을 때.
- 현실에서 보지 못 한 데이터 타입이 등장할 확률이 높다. (Unseen Value를 Tracking 하기 까다롭다.

### 2.2 GLAD
GLAD는 많은 수의 모듈을 가지고 있기 때문에 Scaleup을 하기 쉽지 않은 문제가 있다.

### 2.3 GCE
GLAD의 후속 논문
- Slot-Specific Local encoder들을 하나로 Sharing
- Slot dependent encoding
- 하나의 Encoder만 사용하고 Slot dependent한 encoding을 하게 됨
- scoring 모델은 GLAD와 비슷한 구조
encoding을 할 때 관심 있는 slot 타입에 대해 추가적인 토큰을 부여해 utterance들과 같이 encoding을 하게 된다.

## SUMBT
### 3.1 Overview
- Slot, Value와 독립적인 encodings
- Pre-trained LM 인코더 사용

- 두 종류의 BERT 인코더
    - Dialogue Context Encoder
        a. Trun-level hierarchical encoding
        b. Trainable
    - Slot-Value Encoder
        a. Freeze (as Feature extractor)

- Slot-Utterance Matching Module
- GRU based State Tracker
- Non-parametric Scoring (Enclidean)

### 3.2 Encoding Module
BERT를 이용한 Current turn[r_t, u_t] 인코딩

System Response & User Utterance at current turn step

시스템 발화와 사용자 발화를 인코딩
### U_t = BERT([x^{sys}_t, x^{usr}_t])

BERT_sv를 이용한 Slot, Value 인코딩
- [CLS] 토큰을 이용한 Pooling
- 실제론 Freezed encoder를 통해 미리 Ontology 안의 모든 Slot, Value들을 Pre-encoding 후 Lookup

Ontology에 속하는 Slot, Value들을 미리 vector로 만들고 encoder는 빼버린다.

q^s = BERT_{sv}(x^s),
y^v_t = BERT_{sv}(x^v_t).

### 3.3 Slot-Utterance Matching
Multi-head Attention 을 통한 현재 턴 발화들에 대해 Slot s를 Query로 한 Aggregation
- Query: Slot s vector q^s
- Key: Current Turn t encoding U^t
- Value: Current Turn t encoding U^t

=> h^s_t

### 3.4 GRU-based State Contextualizing
GRU를 이용한 현재 Turn에서 Slot s에 대한 State를 Context turns State에 대하여 Contextualize
- Input: h^s_t == Slot s를 Query로 하여 Turn t를 aggregation한 vector
- Output: d^s_t == 이전 Turn (t-1)에서 Slot s에 대한 hidden state와 gating을 통해 update 된 현재 Turn hidden state
- Layer Normalization을 통해 최종 현재 Turn t에서 Slot s에 대한 representation
**\hat{y}^s_t**

### 3.5 Non-Parametric Scoring
Distance function

