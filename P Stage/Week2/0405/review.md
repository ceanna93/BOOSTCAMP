## 진행 상황
### Imbalance 문제
- 토론 게시판의 ImbalancedDatasetSampler
- F1 Score 확인
- Focal Loss 함수 사용

### 디버깅
- wandb 사용

### 주의해야 할 부분
- train/validation으로 데이터셋을 분리할 때 동일한 사람이 찍은 데이터의 경우 train과 validation에 분리하여 넣지 않도록 해야 validation 값이 정확하게 나오고, 제출한 F1 Score의 값과 유사하게 나온다고 토론에 설명되어 있음. random_split 함수가 아닌 다른 방법으로 train과 validation 분리가 필요.

### 가능하지만 적용하지 못한 방법
- K fold cross Validation
- Onehot이 아닌 Soft labeling -> CutMix, Mixup 등의 방법 사용이 가능

------------------------------------
### 의문
1. GrayScale이 효과가 있을까?
  - 마스크의 색도 다양하기 때문에 검은색은 흰색으로, 흰색은 검은색으로 되기 때문에 큰 차이가 없지 않을까
  - 입고 있는 옷의 디자인/색(현란한 옷을 입는 특정 연령대가 있지 않을까)이 영향을 끼치지 않을까
2. CenterCrop
  - 사진에서 멀리 떨어져서 찍은 사진의 경우 CenterCrop이 효과가 좋겠지만 카메라와 아주 가까이에서 찍은 사진들이 있다. 이러한 사진을 CenterCrop하게 되면 얼굴만 학습에 사용될 수 있다(얼굴만 사용되면 연령을 판단하기 위한 목 주름, 옷, 성별을 판단하는데 많이 사용되는 기준인 머리가 포함되지 않은 위험이 있다고 생각)
3. Shuffle이 필요한 이유(시계열 데이터 제외)
  - [Shuffling data serves the purpose of reducing variance and making sure that models remain general and overfit less.](https://datascience.stackexchange.com/questions/24511/why-should-the-data-be-shuffled-for-machine-learning-tasks)

---------------------------------
Sampler를 쓰게 되면 Shuffle 값을 False로 해줘야 한다.
