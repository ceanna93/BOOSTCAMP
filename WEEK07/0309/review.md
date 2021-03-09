FC(convolutional)L: 입력도 activation map(Tensor), 출력도 activation map 형태. 공간 정보를 유지한 상태로 operation 수행
보통 1x1 convolution으로 구현

각 위치마다 classification을 할 수 있을까.
각 위치마다 채널 축으로 Flattening(Fully-connected)
1x1은 위와 동일한 역할
1x1 convolution kernel이 FC 레이어의 한 weight 컬럼으로 볼 수 있다.
필터 개수만큼 각 위치마다 FC 레이어를 별도로 돌려서 각각의 위치의 결과값을 채워넣는 것과 동일

Stride와 pooling layer로 인해서 최종 activation map의 해상도는 굉장히 저해상도인 경우가 많다.
저해상도 문제를 해결하기 위해 umsampling
stride, pooling을 하지 않으면 똑같은 수의 layer를 사용했을 때, receptive field size가 굉장히 작기 때문에 영상의 전반적인 context를 파악하지 못하는 문제가 있다.
따라서 우선 작게 만들어 receptive field는 최대한 키워놓고, upsampling을 통해 강제로 resolution을 맞춰준다.

결과가 중첩되는 부분이 일정 부분들만 있는데 괜찮은 건지.
Transposed convolution을 사용할 때 주의할 점
=> convolution kernel 사이즈와 stride size parameter를 잘 조절하여 중첩이 생기지 않도록 tuning해줘야 한다.

어려움 없이 쉽게 구현하면서 성능도 좋은 대안이 upsmapling과 convolution을 같이 이용하는 것
upsampling은 중첩 문제가 없고 골고루 영향을 받게 만드는 것

U-Net
Concatenation of feature maps provides localized information
공간적으로 높은 해상도와 입력이 약간 바뀌는 것만으로 민감한 정보를 제공하기 때문에 경계선이나 공간적으로 중요한 정보는 바로 전달하는 중요한 역할을 한다는 것.

What is the spatial size of the feature map is an odd number?
해상도가 일치해야 한다.
Downsample과 Upsample이 빈번하게 일어나는데, 7x7을 Downsample하면 3x3이 되고, Upsample을 하게 되면 6x6이 되면서 원래 입력의 해상도와 차이가 생기게 된다.
따라서 입력을 넣어줄 때 중간에 어떤 map에서도 홀수가 발생하지 않도록 주의해야 한다.
라이브러리나 내부 구현에 따라 downsample이 소수점을 버리거나 반올림할 수 있는 차이가 있다.

의문. Downsample의 최종 결과가 홀수인 것은 괜찮지 않을까

DeepLab
후처리(CRF, Conditional Random Field)의 존재
Atrous(Dilated) Convolution 연산의 사용
실제 convolution보다 더 넓은 영역을 고려하면서도 파라미터 수가 늘어나지 않는다.

Depthwise separable convolution
1. Depthwise convolution
2. Pointwise convolution
효율적인 계산

semantic 보다 유용한 segmentation
Instance segmentation / pontiac segmentation
