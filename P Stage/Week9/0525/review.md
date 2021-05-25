# 강의
## Sequence 모델링
타이타닉은 Non-Sequential Data
Transaction은 Sequential Data(시간 순으로 생성된 데이터)

1. 집계(aggregation), Feature Engineering
		- 집계되는 과정에서 정보들이 손실됨. Feature Engineering이 필수
2. Transaction 그대로 사용 + Feature Engineering
		- 트랜잭션 기반 남녀 예측은 어떤 트랜잭션에 간다고 남/녀 판단이 되는 것이 아니고 전체 트랜잭션(압축)에 따라 남/녀가 결정되어야 한다.
Target이 무엇이냐에 따라 방법이 달라져야 한다.

### Tabular Approach
정형데이터
Feature Engineering
1. 사람의 정답률에 따라 정답여부 예측
2. 문제의 난이도에 따라 학습하고 -1 문제의 난이도로 정답 예측

Train/Valid Data split
- 사용자 단위로 Split해야 사용자의 실력이 보존
- 동일한 사람이 Train과 Valid로 나뉘면 안 된다

### Model Training
- 하이퍼 파라미터보다는 Feature Engineering
- 하이퍼 파라미터는 마지막에 수행.(소수점 자리에서는 하이퍼 파라미터 변경이 의미가 있음)

### Sequential Data
Task 종류에 따라 입출력의 구조를 다르게 가져감
- One-to-One
- One-to-Many (이미지 설명)
- Many-to-One (DKT, DSB)
- Many-to-Many에서 Seq2Seq

### LSTM Example
LSTM을 활용한 주식가격 예측(여러 input을 넣는다면 input size(input의 vector 차원)가 늘어나게 된다.)
- 섹터(범주형 변수)는 integer로 바꾸고 embedding 시켜 그대로 사용하거나, concat하여 2 * embedding size로 만들 수도 있다.

+ Categorical에서 Embedding을 통해 4차원, Reshpae에서 3차원으로 변경, Linear를 통해 [-1, S, X]
+ Continuous에서는 Embedding을 거치지 않고 바로 Linear로 [-1, S, X]
위 두개를 concat하여 [-1, S, 2 * X]가 된다.

### Input Transformation
사용자별로 Sequence를 만들어준다.

Max Sequence length는 하이퍼파라미터. **DKT에서는 padding을 앞에 추가** 
	- 길어도 앞을 자르나? => 앞을 잘라야 마지막 값 예측 가능

#### LSTM + Attention
기존의 LSTM 모델에 Attention Layer를 추가
- mask가 된 부분에 -1000.0(페널티)을 주어 학습이 안 되도록 한다.
- huggingface의 bert 구조

#### BERT
기존의 LSTM 레이어를 BERT로 대체

### FE and Model
1. Feature Engineering 없이 Baseline을 빨리 만든다. (End to End로 input과 output 확인)
2. Feaeture Engineering을 하면서 데이터를 이해
3. K-Fold, Stratified K-fold와 같은 좋은 CV 전략 만들기(CV 점수와 LB 점수의 방향성을 통해 좋은 CV인지 확인)
4. [Feature Selection](https://subinium.github.io/feature-selection/)
	- FE: variance threshold: variance가 적으면 한쪽에 쏠리는 feature
	- Model: recursive feature elimination(RFE), sequential feature selection(SFS)
	- Feature 를 하나씩 넣고 뺴면서 CV와 LB 점수가 오르는지 확인
5. Feature Engineering을 계속 한다.
6. 성능이 향상될 때까지 Model tuning
7. 다른 모델 사용
8. Blending/Stackin/Ensembling(Seed Ensemble도 있다.)
9. 마지막 tuning

베이스라인에는 continuous는 없이 categorical만 있다.

# Competition
### 의문
1. timestamp와, id와 같은 feature를 간단한 값으로 바꿨을 때의 효과. => 캐글의 타이타닉 preprocessing을 보면 연령을 범위로 변경하여 학습한다.
    - https://www.kaggle.com/gunesevitan/riiid-answer-correctness-prediction-eda
2. 데이터는 단순하고 어려운 Task일수록 모델의 성능이 좋아지는 건지.
3. 같은 문제를 얼마나 많은 사람들이 풀었는지에 대한 정보가 학생 A의 점수 예측에 도움이 될지.
4. 예전에 풀었던 유사한 유형의 문제를 풀었을 때 문제의 정답 여부와 경과 시간(log), 유사한 유형에 대한 추세를 학습
5. 접근 방법.
    - 전체 데이터를 넣고 1/0을 출력하는 방법(Many-to-One)
    - Sequential하게 예측하여 가장 마지막에 1/0을 예측하는 방법(Many-to-Many)

### 참고
+ [Correctness prediction paper](https://arxiv.org/abs/2010.12042)
+ [Attention Mechanism](https://arxiv.org/pdf/2102.04250.pdf)
