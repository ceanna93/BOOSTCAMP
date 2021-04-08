# Image classification
## 현재 진행
1. Dataset/Model을 분류하여 ensemble을 하고 inference 과정에서 합치는 방법 시도, 이 때 성별을 제외한 데이터셋은 imbalance하기 때문에 WeightedRandomSampler를 이용하여 학습.
<pre>
  <code>
class MyEnsemble(nn.Module):
    def __init__(self, modelA, modelB, modelC, nb_classes=18):
        super(MyEnsemble, self).__init__()
        self.modelA = modelA
        self.modelB = modelB
        self.modelC = modelC
        # Remove last linear layer
        #self.modelA.fc = nn.Identity()
        #self.modelB.fc = nn.Identity()
        
    def forward(self, x):
        x1 = self.modelA(x.clone())  # clone to make sure x is not changed by inplace methods
        x2 = self.modelB(x.clone())
        x3 = self.modelC(x.clone())
        
        return x1.argmax(dim=-1).item() * 6 + x2.argmax(dim=-1).item() * 3 + x3.argmax(dim=-1).item()
        
  </code>
</pre>

output에 argmax를 사용해줘야 한다. CrossEntropyLoss를 사용하기 위해 output에 argmax를 사용하지 않음.


#### 설정
|| Mask | Gender | Age |
|---|:---:|:---:|:---:|
|epoch| 5	| 3 | 3 |
|model| efficient_b4 | efficient_b4 | efficient_b4|
|sampler| WeightedRandomSampler | X | WeightedRandomSampler |

나머지 파라미터(learning rate 등)는 어제와 동일

\+ 데이터셋을 분류하지 않고 모든 데이터셋을 학습에 사용

#### 결과
|| Accuracy | F1 |
|---|:---:|---:|
|Score| 75.1905%	| 0.6804 |

classifierHead보다 구현이 간단해 보인다.

2. 토론 게시판의 ClassifierHead를 이용한 데이테셋 방법 시도
