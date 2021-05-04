# 수업
## Hybrid Approach
두 가지 접근 방법을 함께 사용

### Ontology based vs Open-vocab based (Recap)
#### Ontology based method
- 각 target slot만다 Candidate-value list가 존재
- Candidate value list로부터 value를 선택함
장점:
- pre-defined ontology를 활용하여 candidate-value list에서 classification을 진행할 수 있음
- Ontology as Prior Knowledge
단점:
- 실제로 ontology / partial ontology에 접근하기 어려운 상황이 존재할 수 있음
- Full ontology에 접근 가능하더라도 slot에 할당된 value가 굉장히 많은 경우 계산 복잡도가 증가함
#### Ontology free method (= Open-vocab based method)
- 미리 정의된 candidate-value list가 없음
- Dialogue context로부터 value를 생성하거나 추출함
장점:
- Ontology에 의존하지 않고 Input source에서 value를 찾아낼 수 있음
- Unseen Slot value Tracking
단점:
- (추출의 경우) Value가 dialogue context에 존재하지 않을 경우 value를 찾아낼 수 없음 (범위를 잘못 찾아내거나 value가 정규화가 되어 있지 않거나 span을 잘못 찾는 경우)
- Value 값이 다양할 경우 적절한 value를 찾기 어려움

## Hybrid Approach
TOD는 정보를 주고 받는 게임.
시나리오에 의해 미리 정의된 시나리오에서 추적을 해야 하는 slot을 slot meta라고 한다.

### Categorical slot
범주형으로 나타낼 수 있는 slot: slot에 할당된 value가 범주형으로 표현 가능한 경우 (Ontology)

선택지 자체가 제한된 경우

### Non-Categorical slot
범주형으로 나타낼 수 없는 slot: Slot value는 unlimited value

Dialogue context 안에서 찾을 수 있음

## DS-DST
Find or Classify?

DS-DST Model
- Ontology based, ontology free(Open-vocab) method를 결합한 Hybrid approach
- Single BERT question answering model을 적용하였음

**두 가지 BERT 모델**
- Encoder
	- BERT는 Trainable한 BERT. Dialogue context를 인코딩하는 BERT는 fine-tuning, Slot-value를 인코딩하는 BERT는 freeze(pre-encoding)
	- Dialouge Context, Slot type을 concat하여 input
=> Span prediction
	- r: hidden output
- Decoder
	- Candidate-Value list에 대해 encoding
	- Fixed BERT model (Trainable X)
	- Slot type과 dialogue context를 함께 인코딩한 어떤 representation과 consine similarity matching을 사용하여 distance function을 사용하여 유사도의 score를 재게 된다. 

DS-DST에서 M(Slot의 개수)을 0으로 지정하면 SUMBT와 동일하게 ontology based가 되는데 일부 slot에 대해 M을 0으로 지정하는 경우 성능이 더 좋게 나온다. (M을 0으로 만들면 DS-Picklist는 Hybrid가 아닌 Ontology based)

non categorical slot의 개수를 몇 개로 지정하는지에 따라 DS, Full ontology, Full open-vocab가 결정된다.

## Prediction & Generation
### DST Computational Complexity
총 J개의 slot에 대한 inference를 진행하고 value 개수까지 따지면 계산 복잡도가 계속 올라가게 된다.

### COMER
간접적으로 DST 모델의 ITC(Inference Time Complexity)를 비교

**COMER Model**
- COMER는 Seq2Seq framework를 적용하여 DST를 Sequence generation 문제로 접근
- 3개의 Encoder와 3개의 hierarchically stacked decoder로 구성
- Single Value Assumption => slot type은 각 turn에서 slot value를 하나밖에 가질 수 없다고 가정(Multi value 상황에 대한 처리가 되지 않는다.)

### NA-DST
TRADE나 COMER 같은 generative 모델은 autoregressive한 decoding을 진행하게 되고 모든 slot마다 decoder를 호출해 step by step으로 생성하는 게 autoregressive 방식

Encoding 이후 한 번에 parallel하게 decoding하는 방식이 Non-Autoregressive한 방식

### SOM-DST
- DST task를 2개의 subtask로 분리
	1. Task1: State operation prediction (Encoder 1개)
	2. Task2: Slot value generation (Decoder 1개)
- Selectively Overwriting Memory (선택적으로 Overwrite)
	- 기존 모델 대비 효율적인 DST Model 구축
	- Slot의 minimal subset (Selective slot)만 가지고 value를 생성할 수 있음

Dialougue Sate
	- B_t

**SOM-DST Model**
State Operation Predictor와 Slot Value Generator로 구성된 모델

Speical Value
	- NULLl: None
	- DONTCARE: 신경 쓰지 않아도 되는 상태
Operation
	- 각 slot에 어떤 변화를 줘야 하는지 결정하는 operation

이전까지 봤던 Operation들은 해당 turn t에서의 decision. SOM-DST의 operation은 이전 turn의 dialogue stae와 현재 turn의 dialouge state 사이에서 발생하는 decision.

Slot -> Operation -> Value (value를 복사, 삭제, 수정)

UPDATE의 경우에만 Slot-value generator에서 generation value를 예측하게 된다.

# Competition
발화 중 에어비엔비를 찾고 있다는 내용이 있는데 이를 숙소로 변경하면 에어비엔비를 숙소명으로 사용하는 부분에서 문제가 될 수 있다.

## 오피스아워
### Huggingface
스타트업 회사에서 NLP를 조금 더 쉽게 하기 위한 라이브러리
Pretrained된 모델을 제공

Trainer is all you need라고 할 수 있지만 위험한 생각

모델 학습
- Configuration
- Tokenizer
- Models
학습 테크닉
- Trainer

Configuration
-> 기존의 어떤 모델이 특정 layer

Model과 Tokenizer는 하나의 SET!

다른 Tokenizer를 사용하면 발생하는 문제
1. 사전 학습된 모델을 사전에 학습된 tokenizer와 동일하게 사용하지 않으면 단어의 이점을 누릴 수 없음
2. 여러 tokenizer를 사용할 경우 special token이 UNK 토큰으로 인식될 수 있음
=> 사전 학습 모델도 다시 학습을 시켜야 할 수 있음

KoBERT의 경우 tokenizer가 huggingface의 tokenizer가 아니다. 기존의 BERT 모델과는 다르다.

**Trainer**
- 더 많은 기능을 쓰려명 Callback을 활용!
Trainer를 Customize하는 방법
1. Trainer를 상속받아 오버라이딩을 진행(Trainer에 있는 함수를 덮어쓰는 방법)
2. 나만의 Trainer를 만든다.(추천)

### Additional Guide
모델 구조 뜯어보기
- 중심이 되는 Pretrained model 뜯어보기
(Huggingface Transformers Document 적극 활용)

왜 + 어떻게 돌아가는지 정확히 파악

DST의 어려움
- 코드 한 줄로 적용하는 것이 불가능
- 기존의 논문을 한국어로 변경하는 작업이 어려움
- SUMBT나 TRADE를 변경하는 작업보다 Dialogue를 이해하는 것을 추천

많은 연구자들이 성능을 높이기 위해 노력하는 것처럼 DST는 어려운 분야고 논문이 가장 최신의 기술을 다루는 것일 수밖에 없다.
=> 강의는 논문으로 구성될 수밖에 없다.

SUMBT와 TRADE를 명확히 이해하면 DST가 어떤 분야인지 경험하는 것을 추천
