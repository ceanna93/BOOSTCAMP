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

### Validation 분리
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
