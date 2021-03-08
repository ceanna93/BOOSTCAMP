AI는 사람의 지능을 컴퓨터 시스템으로 구현하는 것
지능은 인지 능력과 지각, 기억, 이해, 사고와 같은 넓은 능력

지능을 구현하기 위해 가장 첫 번째로 지각 능력의 획득이 가장 중요하다. 
입력과 출력이 사람이 이해하는 형태
=> 사람이 이용할 것이기 때문에

자료구조=>인공지능 분야에선 representation

사람의 시각 인지, 학습에 편향이 있다. 사람의 인지 능력의 장점과 단점을 파악하여 Computer Vision이 발전

사람이 특징을 추출하는 ML보다 AI의 Gradient Discent가 특징을 추출하는 방법이 사람보다 나을 수 있다. 편향이 적기 때문에.

CNN이 나오게 된 이유
1. Fully connected layer에서 국부성의 특징을 추출하지 못하는 문제
2. 파라미터 수 감소

CNN is used as a backbone of many CV tasks

Annotation data efficient learning
Labeling이 모두 되어 있는 데이터를 구축하는 것은 실전에서 딥러닝을 사용할 때의 어려움
Label 데이터의 효율적인 학습 기법의 연구도 하나의 큰 연구 테마

데이터 부족 문제를 완화시킬 수 있는 대표적인 표준 방법들
1. Data augmentation
2. Leveraging pre-trained information
3. Leveraging unlabeled dataset for training

데이터는 거의 모두 bias 되어 있다.
사람이 찍은 데이터는 보기 좋게 찍기 위해 bias된 상태
얻은 training data는 카메라로 찍은 데이터기 때문에 실제 데이터(test data)는 다 표현하지 못하는 데이터

실제 발생 가능한 데이터는 밀도 있게 존재하는데, 취득할 수 있는 데이터는 극히 일부
실제 가능한 데이터로 생각했을 때 학습 데이터에는 빈 공간이 많다.
training dataset과 real data에는 항상 차이가 있다.
데이터 셋이 실제 데이터를 충분하게 반영하지 못한 문제
더 많은 데이터를 모으거나 Data augmentation을 사용하면 차이가 줄어든다.

Cut and Mix를 할 때 영상만 잘라 합성하는 것이 아니라 라벨도 같은 비율로 합성해주는 것이 중요

RandAugment: 랜덤한 augmentation 기법 사용
여러 조합 자동 탐색 알고리즘

어떤 augmentation 기법을 얼마나 강하게 사용할까. 

Leveraging pre-trained information
transfer learning
기존의 미리 학습시켜 놓은 사전 지식을 활용하여 연관된 새로운 태스크에 적은 노력으로도 높은 성능에 도달이 가능한 기술
경제적


데이터가 좀 더 많으면 fine tuning 방법 이용

teacher-student network
- unsupervised learning
- 임의의 데이터 unlabeled data 사용 가능

semantic information is not considered in distillation
내부 요소들의 의미가 중요한 것이 아니라 Soft Label을 따라 하는 것이 중요

Student Loss
Hard label이 Ground truth 데이터셋에서 주어지기 때문에 crossentropy이용
student network가 출력을 한 것과 true label이 일치하도록 만드는 것.
맞는 답을 찾게끔 학습이 된다.

Distillation Loss
KLdiv 사용. 두 개의 Distribution이 있을 때 distribution사이의 차이, 거리를 재는 방법.
Teacher와 Student의 prediction 결과의 차이를 measure를 하고 teacher network가 알고 있는 내용을 따라하도록 만든다.

label이 있는 답을 사용할 때는 Distillation loass와 student loss를 합쳐서 학습


Leveraging unlabeled dataset for training
추가적인 labeling 없이 성능을 올리는 방법
supervised learning에는 labeled 데이터가 필요. 그래서 large scale의 데이터를 구축하는데 한계가 있다.
unlabeled data는 무궁무진한 데이터 사용이 가능
semi-supervised learning은 unlabeled data와 labeled data, 둘 다 활용하는 방법

Self-training
Augmentation + Teacher-Student networks + semi-supervised learning
