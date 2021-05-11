# 강의
TOD와 DST에 내재한 문제와 한계

Predeined Scenario
- 매우 좁은 대화 커버리지
- 제한된 대화의 주도권
- 다양한 가정들
- **Predefined Scenario**에 대한 높은 의존도
Domain extension/transfer

Logical한 처리의 어려움
- 상대적인 표현의 절대적 표현으로의 치환 문제

## 1. Scalability : TOD에서 Scalability를 높이기 위한 노력
### Cost of Dialogue Collection
- Human2Human의 Dialogue 수집은 비용이 매우 비쌈
- 상당한 수의 Annotation Errors를 발생시킴 (MultiWOZ2.1)
- Data Distribution을 제어하는 것이 쉽지 않음 (CoCo)
### User Simulation Approach
- M2M
- Agenda-based Simulation
- Leave-one-out
	Source domains로 학습하고 Target domain에 대해 Evaluation
- Abstract Transaction Dialogue Model

## 2. Robustness : TOD에서 Robustness 측면의 내재된 문제
### Naturalistic Vairation
Natural Conversation Framework

### Counterfactual Goal
데이터셋에서 반영하지 못 하고 있는 Goal (현실에선 나타날 수 있는 경우)

Slot value Distribution in the MultiWOZ

Co-occurrence distribution

CoCo: Utterance Generation Model
