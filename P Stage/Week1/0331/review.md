## Model
- Model with Pytorch

### Model
object, person, system이 대상

### Design Model with Pytorch
#### Pytorch
Open source machine learning framework

Low-level, Pythonic, Flexibility

연구, 공부하기 좋은 프레임워크

변형이 쉽고, 실험이 가능

#### nn.Module
Pytorch 모델의 모든 레이어는 nn.Module 클래스를 따른다.

#### modules
module이 전부 나오게 된다.

#### forward
이 모델(모듈)이 호출되었을 때 실행되는 함수

#### nn.Module Family
nn.Module을 상속받은 모든 클래스의 공통된 특징

모든 nn.Module은 child modules를 가질 수 있다.

#### Parameters
state_dict()
모듈의 파라미터 텐서 확인

각각의 파라미터가 가진 클래스
Tensor base class

requires_grad: True/False

requires_grad에 따라 grad 값이 학습에 따라 갱신이 되지 않을 수도 있다.

### Pytorch가 가진 특징들이 굉장히 많기 때문에 항상 의문점들을 나열, 정리하는 것을 추천

### Pretrained Model
#### Computer Vision의 발전
computer vision의 발전으로 현재 상당히 많은 일을 자동화 할 수 있다.

#### ImageNet
높은 품질의 데이터셋은 필수

Computer Vision 발전에 큰 영향을 끼침

### Pretrained Model
#### 배경
모델 일반화를 위해 매번 수 많은 이미지를 학습시키는 것은 까다롭고 비효율적

좋은 품질, 대용량의 데이터로 미리 학습한 모델을 내 목적에 맞게 다듬어서 사용

미리 학습한 모델을 활용하여 시간을 절약하는 것이 목표

#### 라이브러리
- [torchvision](https://pytorch.org/vision/stable/index.html)
- [timm](https://github.com/rwightman/pytorch-image-models)

### Transfer Learning
pretrained model을 내 목적에 맞게 활용하는 방식
#### CNN base 모델 구조
Input + CNN Backbone + Classifier => Output

- fc(fully connected layer): classfiger

#### 내 데이터, 모델과의 유사성
ImageNet에 있는 Classifier는 1000개의 카테고리

자신이 필요로 하는 모델에 적용이 가능한지 비교하면서 pretrained model을 사용할 것

#### Case by Case
- Case 1. 문제를 해결하기 위한 학습 데이터가 충분하다.
  + Pretrained model(CNN Backbone)이 내 문제와 많이 유사한 경우 CNN Backbone을 Freeze하고 분류하여 inference 속도를 높인다.
  + 유사하지 않은 경우 CNN Backbone을 학습하여 분류하는 것이 성능이 좋다.

  No base에서 시작하는 것보다는 ImageNet pretrained model을 이용하여 학습하는 것이 속도/성능에서 좋을 수 있다.

+ Feature Extraction (Classifier만 변경)
+ Fine Tuning (CNN Backbone + Classifier 변경)

- Case 2. 학습 데이터가 충분하지 않은 경우
  + 상관 관계가 높다면 pretrained model을 사용하는 것을 추천
  + 상관 관계가 낮다면 pretrained model을 사용하지 않는 것을 추천
