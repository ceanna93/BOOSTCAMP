## Training & Inference (1) - Loss, Optimizer, Metric
학습 프로세스에 필요한 요소. 학습에 직접적인 영향을 끼치는 요소

Loss + Optimizer + Metric

### Loss
Loss 함수 = Cost 함수 = Error 함수

### Loss도 사실은 nn.Module Family
nn 패키지에서 찾을 수 있다.

### loss.backward()
모델의 파라미터 grad 값이 업데이트

output과 input의 chain

backward calling -> forward함수

### 조금 특별한 Loss
Custom loss 생성이 가능
- Focal Loss: Class Imbalance 문제가 있는 경우에 사용
- Label Smoothing Loss: Class target label을 Onehot 표현으로 사용하기 보다는 조금 Soft하게 표현해서 일반화 성능을 높이기 위함

### Optimizer
#### 어느 방향으로, 얼마나 움직일 지?

#### LR Scheduler
학습 시에 Learning rate를 동적으로 조절하는 방법
- StepLR
	- 특정 Step마다 Learning rate 감소
- CosineAnnealingLR
	- Cosine 함수 형태처럼 Learning rate를 급격히 변경
	- Local Minima에 빠르게 탈출이 가능
- ReductLROnPlateau
	- 더 이상 성능 향상이 없을 때 Learning rate 감소

### Metric
학습에 직접적인 영향을 미치지는 않는다.

모델을 학습하고 결과를 볼 때 객관적인 지표로 평가
#### 모델의 평가
- Classification
	- Accuracy
	- F1-score
	- precision
- Regression
	- MAE
	- MSE
- Ranking: 추천 시스템에서 많이 사용
	- MRR
	- NDCG
	- MAP

평가 기준이 없으면 모델의 성능을 판단하기 어렵다.

Competition에서는 Metric을 결정하지만 현업에서는 결정해주는 사람이 없기 때문에 데이터에 따라 어떤 Metric을 결정하고 그 Metric을 객관적 지표로 하여 모델을 선택하는 기준으로 제시할 때 사용한다. 따라서 어떤 문제를 보고 Metric을 결정하는 연습이 필요하다.
#### Score의 허와 실
정확도는 데이터 분포가 imbalance할 경우 높아지는 문제가 있다.
- Accuracy: Class 별로 밸런스가 적절히 분ㅍ
- F1-Score: Class 별로 밸런스가 좋지 않아서 각 클래스 별로 성능을 잘 낼 수 있는지 확인 필요

## Training & Inference (2) - Process
학습과 추론 프로세스의 과정을 이해
### Training Process
#### Training 준비
DataLoader -> Model(Pretrained Model) + Loss + Optimizer + Metric

- model.train()
	- Dropout, BatchNorm 등을 조절할 수 있다.
- optimizer.zero_grad()
	- Batch Iter가 돌면서 이전 batch의 grad가 그대로 남게 되는 문제 해결
	- Loss를 현재 batch의 결과로 만들어진 것만으로 구하겠다.
	- Loss를 중첩하여 더하는 것이 기본 (이전 배치에서 loss를 만들어서 grad 파라미터가 업데이트 되면 다음 iter에서 따로 처리가 없으면 loss가 더해진다.)
	- 모델의 파라미터 조절
- loss = criterion(outputs, labes)
	- loss의 grad_fn chain -> loss.backward(): 모델의 파라미터까지 연결
- optimizer.step()
	- optimizer가 input으로 받았던 파라미터 업데이터
	- 실제 데이터에 적용하는 것이 optimizer의 역할

### Gradient Accumulation
메모리를 효율적으로 관리

### Inference Process
- model.eval()
	- self.train(False)
	- Dropout, BatchNorm을 조절
	- eval 이후 inference 진행
- with torch.no_grad()
	- inference 과정에서 파라미터가 업데이트 되면 안 된다.

### Validation 확인
추론 과정에 Validation 셋이 들어가는 것이 검증

#### Checkpoint
각 Validation에서 원하는 loss일 때 저장

### 최종 Output, Submission 형태로 변환
최종 Submission은 스펙을 확인 후 변황하여 제출

카테고리한 클래스를 최종 output으로 변환

## Data Imbalance
- Data Augmentation
- Focal Loss
	- https://pypi.org/project/focal-loss-torch/
	- pip install focal_loss_torch
- F1 Score를 위한 F1 Loss 함수
	- https://gist.github.com/SuperShinyEyes/dcc68a08ff8b615442e3bc6a9b55a354
