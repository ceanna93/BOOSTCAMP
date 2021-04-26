# 수업
## 1. (Task-Oriented) Dialogue System
### 1.1. Taxonomy of dialogue system
Task-Oriented dialogue & Open-domain dialogue (Chit-Chat)

- Dialogue Coverage: 대화를 커버하는 범위.
- Predefined Scenario

**Task-Oriented dialogue:** Predefined Scenario로 task를 정의하게 되고 특정 태스크를 수행해서 성공하게 만드는 것이 목적

**Open-domain dialogue:** 미리 정의된 시나리오가 없이 대화 주제에 제한이 없다. 인간다움, 자연스러움, 답변의 일관성과 몰입도가 목적이다.

#### DST는 Task-Oriented dialogue
### 1.2 Task-Oriented dialogue: Problem Definition
어떤 정보를 유저와 시스템이 주고 게임. 유저 입장에서 정보는 목적이 정의되고 시스템은 유저가 목적을 달성할 수 있게 도와주는 Knowledge Base에 접근할 수 있다.
특정 task에 성공률을 높이는 것이 시스템의 목적이다.

**Predefined Scenario**
Task Schema(시나리오에서 제공하는 정보를 가지고 있는 DB)를 따르게 된다.

### 1.3 TOD: Task Schema
- Informable Slot: 특정 KB instance를 찾거나 새로운 instance를 write하기 위해 User가 System에게 주거나 맥락에 의해 User가 의도할 수 있는 타입의 정보. 대회 시나리오를 제약하는 사항. (User가 System에게 제공).
- Requestable Slot: informable Slot으로 정보를 찾고 난 이후 추가적으로 검색된 KB instance에 대해 물어보거나 정보를 요청할 수 있는 타입의 정보. (System이 User에게 제공).
- User의 Goal은 위 두 개를 목적으로 한다.

Schema는 정해진 양식을 따르지는 않지만 미리 정의된 시나리오를 slot이라는 정보로 표현하게 된다.

### 1.4 Knowledge Base
시나리오를 성공시키기 위해 시스템이 접근할 수 있는 정보.

정의된 task schema를 따르는 DB. 시스템은 user의 목적을 지속적으로 tracking하면서 DB에 접근해 알맞은 정보를 찾아 답변을 만들어줘야 한다.

### 1.6 Components of Modularized TOD System
DM: NLU에서 추출한 정보로 의사 결정을 내리는 부분
- Dialogue State Tracking
- KB 접근
- Dialogue Policy Optimization

## 2. Dialogue State Tracking
### 2.1 Dialogue State
task schema에 의해 미리 정의된 Informable Slot 타입 J개에 대해 User가 의도하고 있는 Value의 상태를 매 turn마다 tracking해야 되는 상태. 즉 J개의 Slot, Value pair의 set으로 표현.

### 2.2 Evaluation Metrics
- Joint Goal Accuracy: turn t에 시스템이 예측한 dialogue와 ground truth의 dialogue 사이의 exact maching. 매우 어려운 metric
- Slot Accuracy: Dialogue state 간의 비교가 아닌 개별 Slot j의 pair level의 accuracy. Joint Goal에 비하면 관대한 metric.

## 3. Properties of DST
### 3.1 Slot Extraction vs DST
||NLU(sot Extractor)|DST|
|:---:|:---:|:---:|
|Input|Dialogue Context|Dialogue Context, slot value, slot type, ...|
|Model's goal|Extract slot value from the input|Estimate all slot values of Predefined slots|
|Tracking abstractive slot value|X|O|
|Utilizing Ontology|X|O/**X**|
|Handling ASR error|X|O|
|Handling State update|X|O|

### 3.2 DST as Entity Extraction
BIO tags를 사용하여 context에 대해 dialogue state를 파악

Abstractive한 속성을 지니는 Boolean Type의 Slot이나 "dontcare"나 "none"과 같은 Special한 Case를 처리하기 위한 추가적인 후처리가 필요

### Entity Typing & Identification
다르게 표현된 value에 대한 표준화가 필요

### Decision making based on Context
여러 turn에 걸쳐 의사 결정이 이루어지기도 한다.

### State Update
매 turn마다 Slot의 value를 추론.
DST는 value의 변화를 감지해야 하기 때문에 State Update 담당
