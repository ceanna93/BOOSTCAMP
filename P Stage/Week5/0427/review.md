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
### U_t = BERT([x
