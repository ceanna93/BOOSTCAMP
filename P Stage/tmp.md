## 시도
- 지난주: 코드 분석
- 주말: R-BERT
- 월/화: ner을 이용한 
- 수: 
- 목: 앙상블

#### Model
- bert-base-multilingual-cased
- koelectra-base-v3-discriminator
- kobert
- R-BERT
- roberta-large
- xlm-roberat-large

#### Augmentation
- 엔티티 순서 변경(바꿨을 때 대칭되거나 동일한 label 증가)
- 새로운 데이터셋 추가(올바르지 않은 label 확인)
- 번역/재번역 데이터셋 추가

#### Tokenize
- 엔티티 사이의 토큰 변경 (두 개의 문장이 아니라 하나의 문장으로 인식하게 만들려는 의도)
- Typed entity marker

#### Hyper parameter
- label_smoothing_factor
- learning_rate
- batch_size
- tokenizer의 max_length
- seed

## 성공/실패 경험
- Transformer 함수 변경

## 어떤 시도를 추가로 해보고 싶은지
- 코드를 깔끔하게 정리하고 싶다. 처음에 유라님의 코드를 통해 하이퍼 파라미터와 모델 변경을 적용할 때까지는 코드가 깖끔했는데 이후 xlm-roberat-large 적용하면서부터 코드가 많이 지저분해졌다.
- wandb를 적용하지 못해 아쉬움
- Q&A 적용을 시도해보지 못 한 점.
- R-BERT를 좀 더 제대로 이해하고 적용했더라면 결과가 달랐을까 의문이 든다. pre-trained된 모델을 사용했을 때 베이스라인 코드와 비슷한 결과가 나오기 때문에 수정하여 다른 모델을 적용했다면 좋은 결과를 기대할 수 있지 않았을까 생각.
- 베이스라인 코드를 크게 벗어나지 못한 부분이 아쉬웠다.

-------------------------

#### 읽어볼 것

https://ratsgo.github.io/machine%20learning/2017/04/24/PCA/

https://ratsgo.github.io/machine%20learning/2017/04/28/tSNE/

https://lovit.github.io/nlp/representation/2018/09/28/tsne/
