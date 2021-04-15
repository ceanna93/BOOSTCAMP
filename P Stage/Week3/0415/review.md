## BERT 모델 학습
BERT 학습의 단계
1. Tokenizer 맏들기
2. 데이터셋 확보
3. Net sentence prediction (NSP)
3. Masking

이미 성능이 좋은데 왜 학습이 필요한가.
도메인 특화 task의 경우, 특화된 학습 데이터만 새롭게 학습하는 것이 성능이 더 좋다.

Dataset: 모델이 학습하기 위한 밥. 재료, 모델의 입력으로 들어갈 수 있는 꼴로 만들어주는 것.
DataLoader: 모델한테 어떻게 밥을 먹여주는지.

### BERT \[MASK\] token 실습
개인정보가 해소된 데이터를 사용해야 하는 이유
- 마스크를 통해 개인정보가 드러날 수 있다. 따라서 개인정보가 해소된 데이터를 이용한 모델을 사용해야 한다.

BERT 로드 후 Tokenizer로 확인 해야 한다.
**언어 모델을 학습할 때 개인정보가 마스킹 처리되거나 개인 정보가 없는 데이터로 학습해야 한다.**

### 한국어 BERT 모델 학습

BertConfig에서 BERT 모델을 정할 수 있다.

BERT에서 다음 문장을 예측하는 학습이 중요하다.

1. Dataset
2. DataLoader
3. Trainer arguments
위 3개를 채우고 학습하는 순서로 실습이 진행.
익숙해지도록 노력할 것.


Tokenizer를 확인 해줘야 하는 이유?

BERT에서 다음 문장을 예측하는 학습이 중요하다?



special token이 필요한 이유. special token을 이용해 pretrained된 BERT 모델에 entity embedding을 추가해도 되는지.
https://github.com/monologg/R-BERT

영어로 학습되어 있는 모델을 사용했을 때 결과.
