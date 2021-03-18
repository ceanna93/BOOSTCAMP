1. 미니 코드
1.1 미니 코드: Floating-point operation

2. 이번 시간 주제
2.1 Fixed point, floating point

지수부, 가수부를 나눌 때 floating point를 많이 사용

fixed point는 곱하기에서 자주 문제가 생긴다.

Precision: Variance
점들끼리 얼마나 떨어져있는지.

Bias: Accuracy
정답으로부터 얼마나 떨어져있는지

2.2 Quantization
- Post-training quantization
- Quantization aware training
- Hardware-aware (mixed precision) quantization

3. 토이 코드
3.1 토이 코드: Layer-wise histogram

## 지식 증류
각각의 스테이지마다 필요로 하는 가치가 다르다.

미니코드: 
Max, atgmax, softmax

Asterisk의 용도

#### Knowledge & decision

의사 결정을 하는 초기에는 지식이 별로 없고, 의사 결정 중요도가 낮아지는 끝에 지식이 많아진다.

빠르게 의사결정을 바꾸는 것(Agile iteratioin)이 필요

### Knowledge distillation
지식을 증류하는 방법

### Teacher-Student networks & Hinton loss
Teacher/Student model과 Transfer learning 차이

Transfer learning
-> 다른 도메인에서 사용한 모델을 적용

#### An example of hard and soft targets
Softmax에 T를 집어넣는 것.
Softened output of ensemble <- the dark knowledge in the ensemble

추론을 할 때 각 출력의 상관관계의 정보까지 모델이 알려준다.

