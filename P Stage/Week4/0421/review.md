## GPT
BERT는 Transformer의 ENCODER, GPT는 Transformer의 DECODER 사용

GPT1이 BERT보다 먼저 나옴

### 분류 Task를 위해 설계된 모델
Linear output layer + softmax

자연어 문장 -> 분류에 성능이 아주 좋은 디코더

fine-tuning에서 만들어지는 목적 함수와 pretrained model을 만드는 비지도 학습의 목적 함수가 같다.

fine-tuning에서 사용되는 layer 자체도 언어

### GPT의 문제를 해결하기 위한 방법
- 인간은 새로운 task 학습을 위해 수많은 데이터를 필요로 하지 않는다.
- Pre-train model -> fine-tuning으로 한 모델이 하나의 task만 수행 가능한 건 자원의 낭비

+ Few-shot, One-shot, Zero-shot은 gradient updates를 하지 않는다.
+ 원하는 task에 대한 힌트를 얼마나 주느냐의 차이

## 개인 공부
Competiton 프로젝트를 Github에 연동하는 것이 가능한지 확인 필요

Soft Voting + 
ner로 구분된 tag를 이용하는 방법을 사용할 수 없을까 시험 (예를 들어, entity1의 ner이 PERSON인데 labeling된 값이 단체:제작 식으로 나오면 당연히 틀린 labeling이기 때문에 이러한 점을 구분할 수 없을지 확인 필요. 하지만 entity2까지 ner 값을 이용하면 결과가 안 좋을 확률이 높아보임. ner이 완벽하지 않아 사람인데, Civilization 또는 O으로 tagging이 되는 경우처럼 올바르지 않은 값으로 tagging이 될 수 있기 때문에. 문장 단위 ner을 적용하면 단체나 사람은 구분을 꽤 정확하게 하는 것으로 보임

(예)
한편, # β ORGANIZATION β bhc치킨#은 배달의민족 ‘@ α PERSON α 배민오더@’ 도입을 기념해 기존 배달 선호 고객을 위한 별도의 프로모션을 마련했다. (오수지_T1124 캠퍼님의 파일)

~~모델이 크기 때문에 각 모델마다 argmax를 하기 전 softmax 값들을 저장하고 모델을 삭제한 후 합치는 방법을 시도할 필요가 있어 보인다. (50G 한계인데 한 모델ㅇ르 저장할 때마다 3G가 필요하기 때문에 세 개의 모델을 저장해 한 꺼번에 inference하기는 어려움.~~

서버의 휴지통을 삭제하면 모델 4개 정도는 저장이 가능할 것으로 예상된다.

각 모델을 분류하여 추론하고 나중에 합치는 방법을 사용할 때 예상되는 장점
1. 용량
2. tokenize 방법을 다르게 해도 된다.
3. 위의 ner 적용이 조금 더 쉽게 느껴진다.

## 오피스아워
- EDA
(Easy Data Augmentation Techniques for Boosting Performance on Text Classification Tasks)
- Back Translation
- Monolingual Semi-Supervised Learning
- Transformer

------------

- 포트폴리오엔 구심점이 필요하다.
  - 오픈소스
  - 블로그
- 문제인식과 문제해결 능력을 어필하기
- 블로그/커뮤니티에 자기 PR
- 과정 Github에 정리
