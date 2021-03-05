## 03/04 피어세션에서 나온 의문
### Seq2Seq에 GAN을 사용할 수 없는 이유
SeqGAN이 있기는 하다.

seq2seq는 Input 차원이 너무 크다.

차원을 줄일 수 있다면 가능하지 않을까.

번역에 Seq2Seq가 많이 사용된다. GAN도 비슷한 방식으로 생성되는데 vision language도 Image -> sequence인데 잘 동작한다. 따라서 동작이 잘 될 것이라고 생각한다.

ImageGAN에서 languageGAN로 변경(강화학습이나 다른 기술을 써서 언어에서 사용하기까지 시간이 오래 걸릴 것이다)

다른 기법들을 써서 생성할 수 있는 모델들을 만든다.

이미지에서 사용한 GAN을 그대로 사용하기는 어렵다.

이산 확률이어서 안된다는 점은 동의하기 어렵다.

Generative와 Adversarial을 강화학습으로.

Input feature이 너무 크다.

일반적인 딥러닝 모델이 다루기에 Seq2Seq는 크다.

된다 안 된다고 구분하기 어렵다.

강화학습을 이용한 Text summarization의 경우 Encoder/Decoder나 Transformation으로 대체되고 있는 추세

## 논문 리뷰
DEEP AUTOENCODING GAUSSIAN MIXTURE MODEL FOR UNSUPERVISED ANOMALY DETECTION
### 논문 구현에서 문제점
loss가 줄어들지 않는다.

저자들이 코드를 공개하지 않으면 구현할 때 어려운 점

loss가 줄어드는 쪽으로 학습이 되는게 딥러닝의 원리인데 loss가 안 주는데 다른 지표가 좋을 수도 있다.

이론적으로는 loss가 줄어들어야 한다.

## 면접 질문
### 유클리디언 거리, 코사인 유사도를 통한 유사도 측정의 차이
- 유클리디언 거리는 공간상에서 실제 거리를 측정하기 때문에 연속형 자료에 활용이 가능하지만 Categorical Data에는 이러한 거리 기반으로 측정하는 것이 옳지 않을 수 있다.
- 인코딩되어 있는 Seq 벡터가 있을 때, 해당 벡터의 크기(norm)는 해당 seq의 의미를 고려하는데 있어서 활용되면 안 될 것이다.
- 따라서 이러한 텍스트 데이터에는 norm으로 표준화시켜주고 각도만을 고려해 유사도를 측정해주는 코사인 유사도를 많이 활용한다.

https://ko.wikipedia.org/wiki/%EC%BD%94%EC%82%AC%EC%9D%B8_%EC%9C%A0%EC%82%AC%EB%8F%84

### 과적합을 막기 위한 딥러닝 기법들
- DropOut
- Early Stopping
- Batch normalization
- Data augmentation
- Label smoothing
- Cross validation
- L1 L2 regularization

### Train 시, Valid, Test를 따로 나누는 이유
- train set으로 학습시키면서 valid set으로 점검하는 과정을 가진다.
- valid set을 이용해 parameter tuning도 할 수 있을 것이고, 학습의 가이드라인을 모델이 알 수가 있다.
- test 데이터까지 Overfitting될 수 있는 문제
- test data는 unseen data로써 이것을 잘 예측하는 것이 목적이기 때문에 train시에 조금이라도 활용되어서는 안 된다
- validation을 이용해 unseen에 대한 성능을 미리 테스트하는 것이 필요
