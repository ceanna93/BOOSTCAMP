## AI + ML과 Quant Trading
100% 자동화 블랙박스

트레디어의 주관이 들어가면 그레이박스

속도 + 알파

속도는 얼마나 빠르게, 알파는 얼마나 똑똑하게

알고리즘은 현업에서 중요하지만 취업에서 요구하는 능력만큼 필요한지는 생각해 볼 일이다.

## AI Ethics
하드웨어나 컴퓨팅 시스템의 발전이 중요하다.

Trade-off TPU 특정 모델에 특화된 하드웨어

하드웨어가 특화가 될 수록 속도와 에너지는 높일 수 있지만 해당 모델에서만 사용이 가능한 하드웨어가 된다. 범용적인 모델이 필요하지 않을까.

어떻게 해야 '좋은' 기술을 만들 수 있는지 생각하기 윤리적인 이슈 생각하기

편견과 윤리 문제에 대해서 깊게 고민하되, 기술 발전을 저지하면 안 된다.

전문가를 대체할 수는 없다는 대답이 인상적이었습니다.

## 특강 외 공부
### CNN이 나오게 된 이유. Fully connected layer만으로 학습하면 안 될까.
Fully Connected Neural Network의 문제점

CNN은 Convolution Layer과 Fully Connneted Layer로 이루어져있다.
CL : 이미지의 특징점을 효과적으로 찾기 위해 사용
FCL: 발견한 특징점을 기반으로 이미지를 분류하는 데 사용

https://aidalab.tistory.com/22
http://taewan.kim/post/cnn/

### Fully Convolutional Network란?
https://yeomko.tistory.com/18

### Stocastic Gradient Descent
Gradient Descent와의 차이점
Gradient Descent는 전체 데이터(full batch)에서 최적의 값을 찾아내는 반면 Stocastic Gradient Descent는 일부 데이터(mini batch)에서 최적의 값을 찾아낸다.
방향성 없이 GD에 비해 더 크게 전진하기 때문에 결과적으로 GD보다 빠르게 Global Minima에 도달할 수 있게 된다.
SGD에 방향성을 갖춘 Optimizer들이 Adam, Momentum 등이 있고, 스텝 크기를 변경하는 게 Adagrad, Adam등이 있다.
https://seamless.tistory.com/38
