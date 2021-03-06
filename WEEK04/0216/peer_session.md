## 02/16 Peer Session

### Q&A
1. (02/15 질문 연장) Word2Vec과 GloVe을 이용한 NLP에서 신조어/문법 파괴 문장에 대한 처리는 어떻게 가능할지. 전처리를 이용해 일반적인 문장으로 변경해야 할 지, 이모티콘 처리는 어렵지 않을지.
    이모티콘과 같은 입력은 묶고 오타 교정 후 처리. 데이터가 적을 경우 오타로 Overfitting이 될 가능성이 있음
    오타, 비문은 Unkown 처리하거나 제거하고 처리한다.

2. GPT3는 스타트업에서 사용하기 어려운지
    일반적으로 스타트업에서 사용하기 어렵다. 많은 데이터로 학습을 시킨 경우 별도로 학습하지 않은 정보도 유추가 가능. (예를 들어, 수박과 메론과 사과의 크기 차이 같은 정보)
    GPT3에 관련하여 자세한 정보를 알고 싶을 때 비판(비난X)하는 글을 읽으면 도움이 된다.
    
3. 정치적인 발언 또는 학습 과정에서 윤리적인 문제가 생겼을 때 대응 방법
    기존의 신경망을 공격하는 방법 등이 있지만 현실적으로 대응하기 어려움
    
4. NLP에서 모델의 크기는 점점 커지는데 Forward의 경우 실시간으로 연산이 가능한지
    실시간 연산 가능

5. NLP 모델에서 실시간 연산이 가능한데 모델 경량화를 하는 이유
    하드웨어가 좋다면 경량화가 필요없겠지만 embedded에서 특히 모델 경량화가 필요하다. edge computing
    
6. 모델은 논문에 작성된 시나리오로 동작하는지. 다르게 작동하는 경우는 없는지.
    일반적으로 논문에 적힌 시나리오로 작동됨.
    
7. 모델을 다른 용도로 사용할 수 있는지.
    사용이 가능할 수도 있음. 하지만 모델 설계자가 의도한 입력과 다른 입력을 이용하여 사용한 경우 사용자의 예상과 다른 출력이 나타날 수 있음.
    특정 모델을 사용할 때 다른 성능이 더 좋은 모델로 대체가 가능한지 생각해보는 자세가 엔지니어에게 필요하다.

### Interview
1. ReLU의 장점
    - 연산 속도, 수렴 속도가 다른 Activation 함수에 비해 빠르다.
    - Vanishing Gradient 문제가 나타나지 않는다.

2. ReLU의 문제점
     - Input 값이 모두 0인 경우 뉴런이 모두 죽어 더이상 값이 업데이트 되지 않을 수 있다.
     - Sigmoid와 공유하는 단점으로 zero-centered가 아니라는 점. 따라서 수렴하고자 하는 위치가 2 또는 4사분면에 존재하는 경우 직선으로 갈 수 없고 zigzag하게 가게 되어 업데이트가 느려지게 된다.

3. bias 사용 이유
     - Input 데이터를 유연하게 처리하기 위해 (네트워크의 유연성)
  
4. CNN에서 Activation FUnction, Batch, Convolution layout, Dropout, Maxpooling의 순서
     - C -> B -> A -> D -> P

5. Train 데이터가 10000개, Test 데이터가 1,000,000개 존재할 때 학습 방법
     - data augmentation
     - 라벨링이 정확한 소량의 데어터와 라벨링이 정확하지 않더라도 대량의 데이터가 학습에 더 효과적이다. 따라서 Train 데이터로 우선 학습을 시키고, Test 데이터를 라벨링한 후, 해당 모델을 삭제하고 라벨링된 Test 데이터로 학습을 다시 진행하는 방법
  
  
  
+ 추가로 알아보기
  - DBSCAN
  - Edge Computing
