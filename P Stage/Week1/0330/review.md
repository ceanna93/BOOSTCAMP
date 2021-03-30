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

## Data Generation
빠른 training과 inference가 가능한 방향성

Data Processing 단계

### Data Feeding
모델 학습을 할 때 모델이 처리하는 양에 비해 데이터 제공량이 부족하면 학습 속도가 떨어지게 된다. Data Generator의 속도가 Model의 성능을 따라가야 한다.

Model의 성능을 높이기 위해서 최소한 Data Generator 속도가 더 빨라야 한다.

두 작업의 속도를 높이는 것이 최상의 성능을 낼 수 있겠지만 현실적으로(GPU, 모델 변경 등) 어렵다.

Dataset 생성 능력 비교
- Compose에 ToTensor + RandomRotation: time 1.28...
- Compose에 ToTensor + RandomRotation + Resize: time 3.65...
- Compose에 ToTensor + Resize + RandomRotation: time 7.87...

Resize 이후 RandomRotation을 할 때 시간이 더 오래 걸리는 이유는 이미지의 용량이 커진 이후 rotate 작업을 처리하기 때문에. 작업의 순서도 속도에 영향을 끼친다.

Resize가 부하를 주기 때문에 Generating 속도가 느려진다.
Compose 안에 transform을 넣을 때도 신중하게 넣고, tuning 해야한다.

### torch.utils.data
#### Dataset
구조
- init: CustomData 클래스가 처음 선언되었을 때 호출
- getitem: CustomData의 데이터 중 index 위치의 아이템을 리턴
- len: CustomData 아이템의 전체 길이

#### DataLoader
Custom Dataset을 효율적으로 사용할 수 있도록 관련 기능 추가

MyDataset -> torch.utils.data.DataLoader -> (Batch, Channel, Height, Width)

- batch_size: 데이터 추출 개수
- num_workers: 사용할 Thread의 개수
- drop_last: batch_size로 나누어 떨어지지 않는 부분을 option에 따라 나머지를 버릴지 결정

병렬 처리와 Batch Size, Rest를 효율적으로 사용하기 위한 util

collate_fn: 사용되는 경우가 많지는 않지만 batch마다 다른 작업을 해주고 싶은 경우 사용. batch 단위마다 다른 작업 적용이 가능

#### Dataset과 DataLoader는 분리되는 것이 좋다.
Dataset안에 DataLoader를 넣지 않는 이유: 재생산성
- Dataset: Vanilla 데이터를 원하는 형태로 출력해주는 클래스
- DataLoader: Dataset을 더 효율적으로 사용하기 위함

DataLoader는 Dataset마다 만들 필요가 없음 (Dataset만 변경하여 DataLoader 재사용 가능)
