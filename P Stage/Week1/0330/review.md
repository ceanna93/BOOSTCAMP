## Dataset
학습에 사용하기 전 단계

문제 해결을 위해 일반화 작업 병행

모델을 위한 dataset이 필요

### Overview
#### 처음 제공된 vanilla data가 dataset으로 변환이 필요
**Data Processing**

Data Anaylysis는 무한 반복

### Pre-processing
시간이 많이 소요되고 Data Science 전체에서 많은 비중을 차지하기 때문에 중요한 작업

이미지는 이미지 용량이 큰 경우 문제가 될 수 있음

CS 지식이 있다면 좀 더 빠르게 엔지니어링 처리가 가능하다는 장점이 있기 때문에 CS 공부 필요

#### Competition Data
보통 경진대회용 데이터는 그 품질이 매우 양호한 편

Data Mining 작업이 거의 필요없는 데이터들

#### Bounding box
noise 제거를 위한 데이터 처리
=> crop

2개의 좌표만 있으면 bounding box 설정 가능

#### Resize
계산의 효율을 위해 적당한 크기로 사이즈 변경

이미지의 용량이 크면 학습이 느려지기 때문에 작업의 효율을 위해 Resize 필요

#### 도메인, 데이터 형식에 따라 다양한 pre-processing이 존재
특히 medical 쪽이 전처리 과정을 통해 좀 더 나은 성능을 보이는 경우가 있다.

### Generalization
#### Bias & Variance
- High Bias (Undefitting)
- Best
- High Variance (Overfitting): 많은 데이터(노이즈)까지 처리

#### Train / Validation
학습을 검증하는 방법
일반화 판단을 위한 과정
학습에 이용하지 않은 분포를 이용해 일반화 확인
Train Set 크기가 부족해도 Validation 하는 것이 필요

#### Data Augmentation
주어진 데이터가 가질 수 있는 Case(경우), State(상태)의 다양성
문제가 만들어진 배경과 모델의 쓰임새를 살펴보면 힌트를 얻을 수 있다.

#### Augmentation 라이브러리
- torchvision.transforms
  + RandomCrop
  + Flip: 사진을 찍을 때 뒤집혀서 찍히는 경우가 존재하는지. Flip으로 마스크 착용 여부를 촬영하는 경우가 존재하는지. 특정 도메인에서는 Flip은 굳이 필요하지 않을 수 있다.
- Albumentations
  + pytorch package는 아님
  + pip package로 설치하는 라이브러리
  + 더 빠르고 다양한 경우를 제공

도메인을 고려해 중요하지 않은 Augmentation 기법은 사용하지 않는다.

'무조건'이라는 단어를 제일 조심할 것!

전처리가 항상 좋은 결과만을 가져다 주는 것은 아님

어떤 데이터 처리든 도메인, 문제에 따라 **실험으로 증명**
