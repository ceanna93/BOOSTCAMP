## 현실 조언

1. 논문 구현 & open source
2. AI Competition 입상
3. AI 프로젝트

위 세개를 어느 정도 이상 해야 입사가 쉬워질 것이다.

## Q & A

1. 차원의 저주가 무엇인지 알고있는지, 설명하고 어떻게 해결할 수 있는지

- 차원의 저주는 모델 예측시 샘플의 수에 비해 변수의 수가 상대적으로 너무 많아서 예측성능이 떨어지는 현상을 말한다
- Feature Selection(Importance기반, Lasso기반 Selection), Dimensional Reduction (PCA, SVD 등 latent Vector 추출 방법)





2. 알고계신 활성화함수들을 말해주시고, 차이점은 무엇이 있는지 등 소개를 해주세요

- 시그모이드 함수 : 입력을 넣었을 때 0~1 사이의 값을 출력하는 함수, binary label일 때 사용 (multi label에서는 soft max함수가 쓰인다)
- 하이퍼볼릭 탄젠트 : -1~1 사이의 값을 출력하는 함수

> 위 두가지는 gradient vanishing Problem

- relu 함수 : 0이하에서는 0의 값을 갖고, 이외의 부분에서는 x 그대로의 값을 갖는 일차선형함수

> leaky relu 등의 0 이하의 값에서 0이 아닌 값을 갖게 하는 활성화 함수도 있다



3. Generalized하게 performance 를 향상시키기 위한 방법에 무엇이 있을지

- 배치정규화
- DropOut
- Cross Valdation (ex. K-Fold CV)
- L1, L2 정규화
- Data Augmentation
- Early Stopping



4. CNN 에서 패딩을 쓰는 이유

- Convolution Layer를 거치면서 이미지의 크기가 점점 작아지게 된다.
- 이는 이미지의 가장자리에 위치한 픽셀들의 정보는 점점 사라지게 되는 문제가 발생시킨다.

- 패딩을 컨볼루션 층 이후에 하는 것과 이전에 하는 것의 차이 : Convolution 과정에서 가장자리에 있는 element는 한번밖에 연산에 포함이 안됨.
- 즉, 패딩을 컨볼루션 이전에 해주지 않는다면 모서리에 있는 element와 중앙쪽에 위치하는 element 사이에 연산에 포함되는 횟수가 너무 많이 차이 나게 되는 현상이 일어나버리게 된다는 것이다.



5. 분류문제에서 손실함수와 활성화함수를 어떤 것을 사용할지, 그걸 사용하는 이유는 무엇일지

- Binary일 때에는 Sigmoid를 활성화함수로 쓰고 binary cross entropy loss 사용, Multi label일 때에는 Softmax를 활성화함수로 쓰고 cross-entropy를 loss 함수로 사용



5-1. logit 이 무엇인가

- 아웃풋이 어디에 배정될지를 구하는 확률값이 목표값이다.
- 이것은 곧 해당 클래스에 배정되는 사건을 성공으로 보고 배정되지 않는 것을 실패로 보는 것
- 이 성공과 실패를 분수꼴로 취한 것이 logit Function



6. normalization 이랑 regularization의 차이

- Normalization은 정규화라는 뜻 (분포를 바꾸어주는 것, 우리가 알고있는 scaling이 그 예시)
- regularization는 규제라는 뜻 (모델의 일반화를 위한, L1 L2 regularization, DropOut, BN 등 모든 과적합을 막기 위한 수단들이 그 예시)
7. R = RNN (d) , R.eval()과 같은 코드에서 eval()메소드가 어떤 역할을 하는지

- 모델에 eval()이라는 메소드를 통해 Train이 아닌 Evaluation 태스크라는 것을 선언해주는 부분이다. (예를 들어, DropOut이 트레인에 적용되었었다면 evaluation 시에는 DropOut된 노드 없이 predict를 수행해야 함)

7-1. no_grad를 쓰는 이유

- 평가시에는 gradient를 역전파로 따로 업데이트할 필요가 없기 때문에, 이를 선언함으로써 시간 비용을 줄일 수 있고 메모리 비용도 아낄 수가 있다.
- gradient값의 저장과 계산과정이 없어지기 때문에 비용과 메모리를 아낄수있다

-------------------------------------------------------
+ Training시에 BN을 Test 시에는 어떻게 쓸 것인가. 저장해 놓은 것을 어떻게 사용하는가. Test에서는 BN을 사용하지 않는다는 무슨 의미인지.
  - 보통 신경망에서 정보들을 합칠 때 각 배치별로 [1.5,2.5,3.5,4.5] 이런식으로 평균이 나온다면 가중평균을 내거나 그냥 평균을 구하는데 사실 테스트 데이터셋에서만 쓰기에 가중평균을 내지 않고 테스트 데이터셋 자체의 평균과 표준편차를 사용하는 것이 아니라 평균으로 각 배치별로 나온 평균의 평균, 표준편차의 평균을 테스트 데이터셋의 배치의 정규화에 사용한다.

+ 구글의 번역기에서 영어 문장에 '.' 을 찍으면 존댓말이 되는 이유
  - 테스트 데이터 자체가 .을 찍었을 때 존대가 되는 경우가 많아서? 따로 '.'을 찍었을 때 존대로 바꾸는 학습을 진행하지는 않았으리라 생각

+ 순전파 갱신을 그래프로 그려주는 도구가 pytorch에 존재하는지. TensorBoard와 같은 것. 계산의 연관성을 나타내는 그래프로 볼 수 있는 방법이 있는지.
  - pytorch에서 텐서보드를 지원
  - https://gaussian37.github.io/dl-pytorch-observe/
