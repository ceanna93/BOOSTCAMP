# 02/23 Peer Session

### Further Question
감염병의 전파를 모델링 하기 위해서는 감염과 더불어 감염된 환자의 회복을 고려해야 합니다. 감염된 사람이 회복될 수 있고, 한 번 감염이 된 사람은 추가적으로 감염이 되지 않는다고 가정한다면 어떻게 전파 모델을 설계할 수 있을까요? 
선형 임계치를 사용하는 것은 불가능
감염이 된 사람은 간선 간의 weight를 0으로 만들면 된다.
회복된 사람은 도려낸다.
edge를 다 잘라낸다.

#### 2^n을 전부 확인해야 하는데 비효율적이지 않나.
감염이 되었다가 회복이 된 경우 더이상 전파가 불가능하기 때문에 비효율적이지 않다고 생각.


### 유튜브 추천 알고리즘이 얼마나 대단한 건지.
이용률이 300% 오르다. 넷플릭스 추천 알고리즘 사용할 수 있는 범위 증가
정형화된 데이터에서만 추천하지만 강화 학습된 애들은 다른 사람들의 추천을 보고 성향을 파악할 수 있지 않나.
카운슬러
추천의 궁극적인 문제
사회 문제 해결

### 추천 시스템 사용
회사에서 원하는 인재들을 추천해주는 시스템 (구인)

AI 면접에서 퇴사율이 높을 지 아닐 지 판단하는 방법

질문에 대한 답변

인사 내부 조직에서도 사용

곧 퇴사할 사람 분류

행동 분석 => 중간 사람이 분석해서 곧 퇴사할 것이라고 예상되는 사람 관리