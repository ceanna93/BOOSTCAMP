## GPT
BERT는 Transformer의 ENCODER, GPT는 Transformer의 DECODER 사용

GPT1이 BERT보다 먼저 나옴

### 분류 Task를 위해 설계된 모델
Linear output layer + softmax

자연어 문장 -> 분류에 성능이 아주 좋은 디코더

fine-tuning에서 만들어지는 목적 함수와 pretrained model을 만드는 비지도 학습의 목적 함수가 같다.

fine-tuning에서 사용되는 layer 자체도 언어

### GPT의 문제를 해결하기 위한 방법
- 인간은 새로운 task 학습을 위해 수많은 데이터를 필요로 하지 않는다.
- Pre-train model -> fine-tuning으로 한 모델이 하나의 task만 수행 가능한 건 자원의 낭비

+ Few-shot, One-shot, Zero-shot은 gradient updates를 하지 않는다.
+ 원하는 task에 대한 힌트를 얼마나 주느냐의 차이

