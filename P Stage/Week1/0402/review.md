## Ensemble
여러 실험을 하다 보면 여러가지 모델로 여러 결과를 만들 수 있다.

현업에서 많이 사용되는 분야는 아니다.

배포를 할 때 효율적인 측면이 중요하기 때문에 여러 모델을 결합하게 되면 모델을 사용하는 시간이 배로 늘어나는 문제가 있기 때문이다.

### Ensemble
(앙상블)
싱글 모델보다 더 나은 성능을 위해 서로 다른 여러 학습 모델을 사용

#### Ensemble of Deep NN
Low Bias, High Variance -> Overfitting

Bias가 높은 모델들을 앙상블 하는 것이 Boosting 기법

Gradient Boosting Algorithm

High Variance 모델들은 Bagging 기법을 사용

#### Model Averaging (Voting)
각각의 모델이 특성을 띄고 있을 때 앙상블이 가장 효과가 있다.

Soft Voting 방식이 일반적으로 Hard Voting에 비해 좋다.

#### Cross Validation
훈련 셋과 검증 셋을 분리는 하되, 검증 셋을 학습에 활용하는 방법

Bias가 커지는 현상을 어느정도 해소할 수 있다.

#### Stratified K-Fold Cross Validation
가능한 모든 경우를 고려 + Split 시에 Class 분포까지 고려

#### Test Time Augmentation (TTA)
테스트할 때 Augmentation

#### 성능과 효율의 Trade-off
앙상블 효과는 확실히 있지만 그 만큼 학습, 추론 시간이 배로 소모

### Hyperparameter Optimization
앙상블 만큼 시간이 오래 걸리지만 성능이 크게 향상되지 않음
#### Hyperparameter
시스템의 매커니즘에 영향을 주는 주요한 파라미터
- Learning rate
- Batch size
- Optimizer
- Loss
- Hidden Layer 개수
- k-fold
- Dropout
- Regularization

파라미터를 변경할 때마다 학습을 해야하기 때문에 시간이 엄청 오래 걸릴 수 있다.

- GradSearch로 점수가 높아지는 방향으로 갱신
- Bayesian Optimization과 같은 optimization 기법

#### Optuna
파라미터 범위를 주고 그 범위 안에서 trials 만큼 시행

## Experiment Toolkits & Tips
### Training Visualization
#### Tensorboard
학습 과정을 기록하고 트래킹

log를 남기고 시각화

#### Weight and Bias (wandb)
딥러닝 로그 기록을 남길 수 있다.

페이지에서 로그 확인 가능

### Machine Learning Project
#### Jupyter Notebook
코드를 아주 빠르게 Cell 단위로 실행, 저장할 수 있는 장점

보통 EDA를 할 때 사용하면 매우 편리하다.

학습 진행 도중 노트북 창이 꺼지면 예전 실행 상태, 로그를 다시 확인할 수 없을 수 있다.
#### Python IDLE
구현은 한번만, 사용은 언제든, 간편한 코드 재사용

디버깅이 jupyter에 비해 강력하다.

자유로운 실험 핸들링

### Some Tips..
분석 코드 보다는 설명글을 유심히 보기.
필자가 생각하고 있는 흐름을 확인

코드를 볼 때 언제든 활용할 수 있을 정도로 디테일한 부분까지 확인

#### Paper with codes
최신 논문과 그 코드까지 확인 가능

많이 공유하면서 자신의 생각을 확인하기
