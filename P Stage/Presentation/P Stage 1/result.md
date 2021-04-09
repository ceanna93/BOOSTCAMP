# \[P stage 1\] 이미지 분류
마스크 / 성별 / 나이 분류 모델을 따로 생성하고 Dataset, DataLoader도 각 모델 별로 생성하여 학습.

세 모델을 학습한 이후 추론에서 이미지 별로 세 모델의 결과를 하나로 합쳐주도록 구현

## Dataset
<pre>
<code>
class MaskDataset(Dataset):
    def __init__(self, image_dir, transform=None):
        self.image_dir = image_dir
        self.transform = transform
        
        self.image_paths = []
        profiles = os.listdir(self.image_dir)
        for profile in profiles:
            if remove_hidden_file(profile):
                for file_name in os.listdir(f'{image_dir}/{profile}'):
                    img_path = os.path.join(image_dir, profile, file_name)
                    if is_image_file(img_path):
                        self.image_paths.append(img_path)
        
        self.image_paths = list(filter(is_image_file, self.image_paths))
        self.image_paths = list(filter(remove_hidden_file, self.image_paths))
        
        self.labels = [get_mask_label(path) for path in self.image_paths]
        
    def __getitem__(self, idx):
        image_path = self.image_paths[idx];
        label = self.labels[idx]
        image = get_img(image_path)
        
        if self.transform:
            image = self.transform(image = image)['image']
        #label = torch.eye(18)[label]
        return image, label
    
    def __len__(self):
        return len(self.image_paths)
</code>
</pre>

## Transform
<pre>
<code>
def get_transforms(need=('train', 'val'), img_size=(512, 384), mean=(0.548, 0.504, 0.479), std=(0.237, 0.247, 0.246)):
    transformations = {}
    if 'train' in need:
        transformations['train'] = Compose([
            CenterCrop(448, 336, p=1.0),
            Resize(img_size[0], img_size[1], p=1.0),
            HorizontalFlip(p=0.5),
            ShiftScaleRotate(p=0.3),
            HueSaturationValue(hue_shift_limit=0.2, sat_shift_limit=0.2, val_shift_limit=0.2, p=0.3),
            RandomBrightnessContrast(brightness_limit=(-0.1, 0.1), contrast_limit=(-0.1, 0.1), p=0.3),
            Normalize(mean=mean, std=std, max_pixel_value=255.0, p=1.0),
            CoarseDropout(p=0.3),
            GaussNoise(p=0.3),
            Cutout(p=0.3),
            ToTensorV2(p=1.0),
        ], p=1.0)
    if 'val' in need:
        transformations['val'] = Compose([
            CenterCrop(448, 336, p=1.0),
            Resize(img_size[0], img_size[1], p=1.0),
            Normalize(mean=mean, std=std, max_pixel_value=255.0, p=1.0),
            ToTensorV2(p=1.0),
        ], p=1.0)
    return transformations
</pre>
</code>

## 모델
Pretrained된 EfficientNet b4 모델 사용

## 손실함수
CrossEntropyLoss

## Optimizer
AdamP

## DataLoader
<pre>
<code>
mask_train_dataset = MaskDataset(img_dir, transforms['train'])

mask_counter = Counter(mask_train_dataset.labels)
mask_class_count = [i for i in mask_counter.values()]
mask_class_weights = 1./torch.tensor(mask_class_count, dtype=torch.float)
mask_class_weights_all = mask_class_weights[mask_train_dataset.labels]

mask_weighted_sampler = WeightedRandomSampler(
    weights=mask_class_weights_all,
    num_samples=len(mask_class_weights_all),
    replacement=True
)

mask_train_loader = DataLoader(mask_train_dataset, batch_size = conf.batch_size, shuffle=False, num_workers=3, sampler=mask_weighted_sampler)
</code>
</pre>

**Counter**를 이용해 MaskModel의 분포를 확인하고 WeightedRandomSampler 생성

Gender의 경우 데이터의 개수가 거의 동일하기 때문에 Sampler 없이 Shuffle만 True로 설정

## Train
<pre>
<code>
mask_scheduler = StepLR(mask_optimizer, lr_decay_step, gamma=0.5)


os.makedirs(os.path.join(os.getcwd(), 'results', mask_name), exist_ok=True)

counter = 0
patience = 10
accumulation_steps = 2
best_val_acc = 0
best_val_loss = np.inf
for epoch in range(num_epochs):
    # train loop
    MaskModel.train()
    loss_value = 0
    matches = 0
    for idx, train_batch in enumerate(mask_train_loader):
        inputs, labels = train_batch
        inputs = inputs.cuda()
        labels = labels.cuda()

        outs = MaskModel(inputs)
        pred = outs.data.cpu().numpy()
        preds = torch.argmax(outs, dim=-1)
        loss = criterion(outs, labels)

        loss.backward()
        
        # -- Gradient Accumulation
        if (idx+1) % accumulation_steps == 0:
            mask_optimizer.step()
            mask_optimizer.zero_grad()

        loss_value += loss.item()
        matches += (preds == labels).sum().item()
        if (idx + 1) % train_log_interval == 0:
            train_loss = loss_value / train_log_interval
            train_acc = matches / conf.batch_size / train_log_interval
            current_lr = mask_scheduler.get_last_lr()
            print(
                f"Epoch[{epoch}/{num_epochs}]({idx + 1}/{len(mask_train_loader)}) || "
                f"training loss {train_loss:4.4} || training accuracy {train_acc:4.2%} || lr {current_lr}"
            )
            
            if train_acc > best_val_acc:
                print("New best model for val accuracy! saving the model..")
                torch.save(MaskModel.state_dict(), f"results/{mask_name}/{epoch:03}_accuracy_{train_acc:4.2%}.ckpt")
                best_val_acc = train_acc
                counter = 0

            loss_value = 0
            matches = 0

    mask_scheduler.step()
</code>
</pre>

Validation 없이 전부 학습에 사용

## Inference Model
<pre>
<code>
class MyEnsemble(nn.Module):
    def __init__(self, modelA, modelB, modelC, nb_classes=18):
        super(MyEnsemble, self).__init__()
        self.modelA = modelA
        self.modelB = modelB
        self.modelC = modelC
        
    def forward(self, x):
        x1 = self.modelA(x.clone())  # clone to make sure x is not changed by inplace methods
        x2 = self.modelB(x.clone())
        x3 = self.modelC(x.clone())
        
        return x1.argmax(dim=-1).item() * 6 + x2.argmax(dim=-1).item() * 3 + x3.argmax(dim=-1).item()
        
        
ensemble = MyEnsemble(MaskModel, GenderModel, AgeModel)
</code>
</pre>


테스트/제출 코드는 동일

|Accuracy|F1|
|:---:|:---:|
| 76.3968% | 0.6842 |
