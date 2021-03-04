1 standard scaler와 minmax scaler의 장단점, 단점의 해결방법
StandardScaler 와 MinMaxScaler는 이상치에 민감하게 scaling되어 분포를 그대로 유지하지 못하게 된다.

RobustScaler : 평균 대신 중앙값을 씀으로써 보다 분포형태를 유지하게끔 scaling을 할 수 있게 된다.

참고 : https://mkjjo.github.io/python/2019/01/10/scaler.html

개인적인 추가 질문
  + normalization에서 min-max와 z-score 기법을 같이 사용하는데 scaler도 같이 사용할 수 있는지.
  
    같이 사용이 가능하다. RobustScaler의 경우 되도록 원래 분산을 유지하는 형태로 scaler가 되는데, 반드시 원래 분산의 형태를 유지하는 것이 좋은 것은 아니다. 적절히 다른 scaler와 같이(예를 들어, min-max scaler) 사용하면 도움이 된다. 2개 이상의 scaler를 사용할 땐 반드시 결과를 확인하고 사용할 것.

2 GAN이 Seq2Seq모델에 적용가능한지

Seq2seq의 결과는 이산 확률 분포이기 때문에 적용할 수 없다.

하지만 Electra모델은 GAN의 아이디어를 학습에 이용하였다. Adversarial 하게 학습하지는 않는다.

아래는 현재 추측
※ GAN을 seq2seq에 적용할 수 없는 이유 정리

GAN은 Continuous Data를 생성해내는 것에 대해서는 잘 작동하였다.

하지만 만약 GAN을 seq2seq모델에 적용한다면, Generator를 통해 생성되어야 하는 sequence의 형태가 discrete여야 할 것이다.

다시 말하자면 이는 discrete를 생성하는 Generator -> Discrminator까지의 과정에서 가중치 업데이트를 역전파법을 사용해서 수행해야 한다는 것이다.

이 부분을 세부적으로 살펴보면 Generator가 생성할 수 있는 값은 softmax를 통한 확률을 나타내는 연속적인 값에 불과할 것이고, 공간상에서 이 값과 그나마 유사한 seq를 찾아 generate를 수행하게 될 것이다.
하지만 공간상에서 유사한 seq를 찾는 부분은 역전파법을 통해 딥러닝 모델이 학습할 수가 없는 부분이다.

따라서 GAN을 seq 모델에 적용할 수가 없다.

※ 만약 위의 정리된 내용(GAN을 seq2seq에 적용할 수 없는 이유)이 맞다면, 이에 이어지는 질문
사실 공간상에서 이 값과 그나마 유사한 seq를 찾는 과정을 생각하지 않고, Generator 과정에서 나온 softmax 값까지만을 이용해서 Discriminator가 판별하게끔 모델의 구조를 짠다면 충분히 GAN을 seq2seq에 적용할 수 있지 않을까요?

3. Multi head attention에서 matmul을 사용하는데 고차원에선 이러한 곱연산이 어떻게 이루어지는가? (예를들어 3, 4차원 정도의 고차원일 경우 matmul연산이 어떻게 이루어지는가?)

A는 7x5x4x3 차원, B는 7x5x3x4 차원일 때 결과는 7x5x4x4의 shape이 나온다.

이는 뒤의 두 dimension이 나타내는 행렬의 차원의 곱이 성립하고, 이외에 앞의 shape (위의 경우는 7x5, 7x5이므로 같음)이 모두 같다면 곱 연산이 가능하다.

참고 : https://ebbnflow.tistory.com/159

np.dot 함수는 dot product로서 내적연산(벡터내적과 같은)을 한다고 알고 있었는데 고차원에서의 np.dot연산의 결과는 다음 코드를 보면 오히려 차원이 추가되어버리는 것(?) 같아서 이해가 잘 되질 않음
>>> import numpy as np
>>> A = np.arange(2*3*4).reshape((2,3,4))
>>> B = np.arange(2*3*4).reshape((2,4,3))
>>> np.dot(A,B).shape
(2, 3, 2, 3) 

4. CNN에서 층을 많이 쓰면 좋다고 알려져있는데 왜 막상 많이 쌓으면 안좋은가, 이를 어떻게 해결했는가?

층이 많아지면 파라미터가 계속해서 곱해지면서 작아지니까? 앞단의 정보가 희석이 되니까 이를 해결하기 위해 만든 것이 ResNet 모델이다. 이것은 구조상 아웃풋에 x를 더해줌으로써 CNN층을 더욱 깊게 쌓더라도 전층의 정보를 유지할 수 있게 하였다.

1X1 convolution layer를 쓰는 이유 : 원래의 형상을 유지할 수 있어 성능은 유지하면서도 파라미터 수를 줄일 수가 있다.

5. LSTM과 GRU의 차이는?

Cell state가 없다,  GRU는 게이트가 2개이고, LSTM은 3개이다. (LSTM에 있는 출력 게이트가 없다)

6. Word Embedding이란?

컴퓨터가 텍스트를 인식할 수 없으니까 수치화 시켜주는 것

예시로 tf-idf, Word2vec과 Glove 등이 있다.

6-1. One-hot Encoding보다 Word Embedding이 좋은 이유

단어간 연관성을 반영할 수 있다

Embedding 차원만큼만 학습하면 되므로 연산상에 이득이 있다.

6-2. word2vec 을 딥러닝 모델이라고 볼 수 있나요??

은닉층이 하나밖에 없고 활성화함수가 없기 때문에 딥러닝이 아니다

7. Bias-Variance Trade off가 무엇인지 과적합과 연관지어 설명해보기

Bias는 train시 y와 predict 값의 차이를 의미한다.

이 Bias를 줄이는 것으로 너무 과대적합을 하게 되면 Variance가 높게 되는 경우가 생기며, 다시 Variance를 낮추기 위해 노력하면 Bias가 높아지는 현상이 생기는데 이것을 Bias-Variance Trade off라고 한다.

결국 Bias와 Variance 두 가지가 합리적으로 함께 낮은 지점을 찾도록 노력해야 한다.
