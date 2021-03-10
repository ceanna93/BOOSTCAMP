Object detection

semantic과 instance/panoptic의 차이는 instance(같은 객체여도 다른 물체)를 구분을 하는가
panoptic은 instance를 포함

Two-stage detector
Gradient-based detector
영상의 경계, Gradient를 기반으로 한 detector 유행
최근까지 많이 사용한 방법은 Selective search
다양한 물체 후보들에 대해서 영역을 특정해서 제안해주는 방식
Bounding box
Box proposal
1. 영상을 비슷한 색끼리 잘게 분할
2. 비슷한 색, Gradient의 특징, 분포가 비슷한 영역끼리 반복해서 합쳐주기
3. 큰 segmentation들을 포함하는 bounding box를 추출해서 물체의 후보군으로 사용

딥러닝을 이용한 초기 물체 탐지에도 초반의 bounding box를 제안해주는 neural network모델이 제안되지 않아 Selective search가 많이 사용

R-CNN
1. Selective Search로 region proposals 구하기
2. 각 Region proposal를 CNN의 적절한 크기로 warping
3. CNN에서 카테고리 Classification
4. FC layer에서 추출된 feature를 기반으로 SVM만을 학습해서 사용

단점은 각각 region proposal마다 모델에 넣어서 학습을 해야하기 때문에 속도가 굉장히 느리다
region proposal은 별도의 핸드 디자인된 알고리즘을 사용해, 학습을 통한 성능 향상에 한계가 있다.

Fast R-CNN
영상 전체에 대한 feature를 한 번에 추출하고 이를 재활용하여 여러 object를 detection
여전히 region proposal은 selective search를 사용

Faster R-CNN
region proposal을 개선
neural network 기반으로 대체
최초의 end-to-end 모델

IoU 두 영역의 교집합을 측정하는 기준을 제공하는 방법
교집합/합집합

region proposal
=> Anchor boxes
각 위치에서 발생할 것 같은 박스들을 미리 정의한 후보군들
비율과 스케일이 다른 영역을 각 위치마다 미리 정해놓고 사용
(가변적인 파라미터)

RPN(Region Proposal Network)
feature map 관점에서 fully convolution하게 sliding window 방식으로 얻으면서 매 위치마다 k개의 anchor box를 고려.
anchor box 후보 k개를 고려할 때 각 위치에서 256-dimension의 feature 벡터 하나를 추출하고 여기서 2*k개 classification score를 확인하고 k개의 bounding box의 정교한 위치를 regression하는 regression branch가 따로 존재.
4*k개의 regression output이 출력된다.
4*k개인 이유
bonding box 하나를 정의하기 위해 왼쪽 위 꼭지점 좌표와 너비, 높이 정보가 필요하기 때문에 4-dim

anchor box를 미리 정의했는데 그것을 사용하지 않고 왜 다시 박스를 regression하는지.
anchor box를 촘촘하면 문제가 되지 않지만 계산 속도가 느려지고 적당한 양의 anchor box만 미리 만들어두고 정교한 위치는 regression으로 해결
<분할 정복>
학습할 때는 objectness classifier는 classifcation loss(cross entropy)를 사용

box coordinates regression의 경우 regression loss를 사용
두 loss가 RPN을 위한 것

2*k는 Object인지, Non-object인지 각각의 anchor 박스에 대해서 구별을 하는 형태로 classification score가 나온다.

Deep Learning에서도 Bounding box를 filtering하기 위해 NMS(Non-Maximum Suppression) 알고리즘 사용

One-stage(Single) detector

정확도를 조금 포기하더라도 속도를 높이는 것이 목적
RoI pooling을 사용하지 않고 곧바로 Box regression과 Classification을 사용

YOLO는 가장 마지막 레이어에서 한 번만 Prediction을 하기 때문에 localization 정확도가 떨어지는 문제점이 있다.
이를 보완하기 위해 SSD(Single Shot MultiBox Detector)

multi scale object를 더 잘 처리하기 위해 중간 feature map을 각 해상도에 적절한 bounding box들을 출력할 수 있도록 multi scale 구조를 만들었다.

Two-stage detectore VS One-stage detector
Single-Stage 방법은 모든 영역에서의 loss가 계산되는 문제
일반적인 영상에서는 background의 영역이 더 넓다.
positive sample은 엄청 적은 반면 배경은 유용한 정보도 없으면서 class imbalance 문제를 발생시킨다.
=> Focal loss를 제안
(Cross Entropy의 확장)


현재 연구 트렌드
Detection with Transformer
Detecting objects as points
