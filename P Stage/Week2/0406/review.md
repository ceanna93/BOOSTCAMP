## Image Classification
### 진행상황
- ImbalancedDatasetSampler 적용
- EfficientNet 7
- epoch 50
- learning rate 1e-4
- focal loss
- early stopping으로 11 epoch에서 정지

#### 결과
|| Accuracy | F1 |
|---|:---:|---:|
|Score|74.2857%	| 0.6568 |

### 현재 학습
#### Validation 분리
<pre>
  <code>
os.makedirs(os.path.join(os.getcwd(), 'results', name), exist_ok=True)

image_dir = os.path.join(conf.data_dir, 'images')

for fold_idx in range(conf.n_fold):
        train = info[info.fold != fold_idx].reset_index(drop=True)
        val = info[info.fold == fold_idx].reset_index(drop=True)

        transforms = get_transforms()
        train_dataset = MaskDataset(image_dir, train, transforms['train'])
        val_dataset = MaskDataset(image_dir, val, transforms['val'])
        train_loader = DataLoader(train_dataset, batch_size = batch_size, shuffle=True, num_workers=3)
        val_loader = DataLoader(val_dataset, batch_size = batch_size, shuffle=False, num_workers=3)
        
        fit(train_dataset=train_dataset, valid_dataset=val_dataset, train_loader=train_loader, valid_loader=val_loader)
  </code>
</pre>

위와 같이 K-Fold를 이용하여 train_loader와 validation_loader 생성([이현수 멘토님 토론](http://boostcamp.stages.ai/competitions/1/discussion/post/57))

K-Fold와 Epoch이 있을 때, K-Fold 내부에 epoch을 돌린다.

fit 함수를 별도로 만들어 생성한 train_loader와 validation_loader를 파라미터로 넘겨준다.

K-Fold 5, epoch 10 training...

#### Transform
- CenterCrop
- CutMix

### 시도해볼 수 있는 방법
작은 파라미터의 모델 사용 (피어세션에서 데이터셋이 작은 경우 파라미터가 큰 모델을 사용할 때 변수가 잘 설정되지 않아 학습이 잘 되지 않을 수 있다는 설명)

#### Loss function
Cross Entropy + WeightedRandomSampler

#### 모델 분류에서 세 분류 방법에 따라 모델을 분류하는 것이 성능 향상에 도움이 될까
나이 분류 모델을 찾을 때 '나이 + 성별'을 함께 분류하는 경우가 많다. 성별에 따라 나이의 특징이 달라지기 때문이 아닐까 생각이 들었다. 따라서 \[마스크\] + \[성별 + 나이\]로 분류 모델의 성능을 확인할 필요가 있어 보인다.

1

## Image Classification

2

### 진행상황

3

- ImbalancedDatasetSampler 적용

4

- EfficientNet 7

5

- epoch 50

6

- learning rate 1e-4

7

- focal loss

8

- early stopping으로 11 epoch에서 정지

9



10

#### 결과

11

|| Accuracy | F1 |

12

|---|:---:|---:|

13

|Score|74.2857% | 0.6568 |

14



15

### 현재 학습

16

#### Validation 분리

17

<pre>

18

  <code>

19

os.makedirs(os.path.join(os.getcwd(), 'results', name), exist_ok=True)

20



21

image_dir = os.path.join(conf.data_dir, 'images')

22



23

for fold_idx in range(conf.n_fold):

24

        train = info[info.fold != fold_idx].reset_index(drop=True)

25

        val = info[info.fold == fold_idx].reset_index(drop=True)

26



27

        transforms = get_transforms()

28

        train_dataset = MaskDataset(image_dir, train, transforms['train'])

29

        val_dataset = MaskDataset(image_dir, val, transforms['val'])

30

        train_loader = DataLoader(train_dataset, batch_size = batch_size, shuffle=True, num_workers=3)

31

        val_loader = DataLoader(val_dataset, batch_size = batch_size, shuffle=False, num_workers=3)

32

        

33

        fit(train_dataset=train_dataset, valid_dataset=val_dataset, train_loader=train_loader, valid_loader=val_loader)

34

  </code>

35

</pre>

36



37

위와 같이 K-Fold를 이용하여 train_loader와 validation_loader 생성([이현수 멘토님 토론](http://boostcamp.stages.ai/competitions/1/discussion/post/57))

38



39

K-Fold와 Epoch이 있을 때, K-Fold 내부에 epoch을 돌린다.

40



41

fit 함수를 별도로 만들어 생성한 train_loader와 validation_loader를 파라미터로 넘겨준다.

42



43

K-Fold 5, epoch 10 training...

44



45

#### Transform

46

- CenterCrop

47

- CutMix

48



49

### 시도해볼 수 있는 방법

50

작은 파라미터의 모델 사용 (피어세션에서 데이터셋이 작은 경우 파라미터가 큰 모델을 사용할 때 변수가 잘 설정되지 않아 학습이 잘 되지 않을 수 있다는 설명)

51



52

#### Loss function

53

Cross Entropy + WeightedRandomSampler

54



55

#### 모델 분류에서 세 분류 방법에 따라 모델을 분류하는 것이 성능 향상에 도움이 될까

56

나이 분류 모델을 찾을 때 '나이 + 성별'을 함께 분류하는 경우가 많다. 성별에 따라 나이의 특징이 달라지기 때문이 아닐까 생각이 들었다. 따라서 \[마스크\] + \[성별 + 나이\]로 분류 모델의 성능을 확인할 필요가 있어 보인다.

57



58

나이와 성별을 분리한다면 나이는 linear regression 방법나이와 성별을 분리한다면 나이는 linear regression 방법
