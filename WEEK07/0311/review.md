Instance sementation
= Semantic segmenatioon + distinguishing instances
개체의 구분

Mask R-CNN
RPM을 이용해 RoiPooling을 이용하는 것이 아니라 RoIAlign pooling 레이어를 제안
소수점 픽셀 레벨 풀링을 제안
성능 개선

Mask R-CNN = Faster R-CNN + Mask branch

Panoptic
= Stuff + Instances of Things
배경 정보, 관심을 가질 만한 물체들의 instance까지 구분해서 segmentation

Semantic & Instance head -> Panoptic head -> Panoptic logits

Landmark localization
각 픽셀별 Classification
= keypoint estimation: Predicting the coordincates of keypoints

Coordinate regression: usually inaccurate and biased 일반화의 문제
Heatmap classification: better performance but high computational cost

sementic segmentation처럼 한 채널들이 각각의 keypoint를 담당
각 keypoint마다 하나의 클래스로 생각을 해서 keypoint가 발생할 확률 맵을 각 픽셀별로 classification하는 방법

Conditional generative model
P(X|sketch of a bag)
조건이 주어지고 조건에 해당하는 결과가 나온 것
확률 분포를 모델링

사용자의 의도가 반영된 생성 방식

1. 저품질 오디오를 고품질 오디오로 변경
2. 번역
3. 제목과 부제목이 있을 때 나머지 글을 생성

Style transfer, Supter resolution, Colorization

GAN은 data의 dependency가 생기게 된다
Perceptual loss
학습과 코딩이 편하다.
pre-trained network를 사용해야한다.

pre-trained의 early layer들은 이미지를 perceptual space로 변환하는 Transform.
