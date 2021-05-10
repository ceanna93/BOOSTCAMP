# 강의
## Taxonomy of DST models
Ontology-based는 volume에 따른 complexity와 Unseen slot value tracking이 어려움.

Open-vocab DST는 또 다른 종류의 복잡도와 생성으로 인한 오류가 있다.

둘을 합친 Hybrid DST

## TripPy
Triple Copy Strategy
1. Span-based Copy mechanism
2. System Inform Memory for Value Prediction
3. DS memory for Coreference Resolution

### Motivation
복잡한 Dialogue일수록, 지칭하는 사람, 동의어, Slot-Value 등이 여러 turn에 복잡하게 얽혀 있을 가능성이 높다.

DST span으로 처리하는 경우 오히려 성능이 떨어지는 문제.
=> Ontology의 추가적인 도움이 필요

Tripy는 위 결점을 보완

### Slot Gates
none, dontcare, span, inform, refer

inform: system이 inform한 value에 대해 user가 긍정적(Confirm)으로 답했을 때 (시스템이 제시한 조건을 사용자가 수락했을 때)
refer: user가 이전 turn의 dialogue에서 inform한 value와 동일한 vlaue일 때 (!=CARRYOVER)

- s: 각 slot-type마다 CLS vector를 넣어 5개의 Classification을 한다.

SOM-DST와는 다르게 각 slot type마다 독립적인 파라미터(runnable한 파라미터)를 갖고 있다.

#### Boolean type gate
none, dontcare, true, false

bgate는 slot마다 가지게 된다. (파라미터 수 증가)

### Span-based Value Prediction
start에 softmax를 취해 distribution를 구하고 end도 마찬가지 방법으로 distribution을 구하고 argmax를 하여 span을 추출

Slot Get Classification의 결과 "span"으로 예측된다면, 추출된 span의 결과를 현재 턴 Slot의 value로 copy

### System Inform Memory for Value Prediction
Turn t에 system에 의해 inform된 Slot의 value

Slot Get Classification의 결과 "inform"으로 예측된다면, Inform Memory에서 value로 copy

System의 발화가 중요

### DS Memory for Coreference Resolution
type간의 reference가 일어나는 경우

Slot Meta + No reference(1)
: N + 1

이전에 채워진 State의 어떤 Slot에서 Value를 Copy해올지 Classification

### Experiments
history를 다 넣어주는 게 중요

# Pretraining
## TOD-BERT
장점은 데이터가 적을 때 특화해서 좋은 성능을 보임

## ConvBERT
DialoGLUE
- Target dataset 이용해서 추가로 Pre-training (MLM)
- 두 가지 방법:
	- Pre-training 후 Fine-tuning
	- Pre-training과 동시에 Fine-tuning
Few shot에서 좋은 성능

### SimpleTOD

# Competition
적용하기 어려운 SOM-DST 문제들

어떤 조건으로 inference 과정에서 id 뒤에 숫자가 포함되는지. eval_dials의 첫 번째 dialouge를 보면 대화의 개수는 8개(사용자, 시스템 대화를 한 개로 계산)로 8개의 dialogue state가 predection 파일에 저장되어 있음
