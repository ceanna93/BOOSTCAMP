## BERT 언어 모델 기반의 문장 토큰 분류
주어진 문장의 각 토큰이 어떤 범주에 속하는지 분류하는 task

문장이 입력으로 들어가면 각 토큰마다 Classification Layer가 부착되어 각 토큰이 어떤 토큰인지 분류하는 task
- NER: Named Entity Recognition
    문맥을 고려하는 것이 중요
- Part-of-speech tagging (POS TAGGING)
    형태소, 의미학적으로 최소한의 단위로 파악

### kor_ner
- 한국어 NER 데이터셋

## 문장 토큰 분류 모델 학습
NER fine-tuning with BERT

형태소 단위로 토큰을 음절 단위의 토큰으로 분해하고, Entitiy tag 역시 음절 단위로 매핑시켜 주어야 한다. (추천)

## 시도
학습을 할 때 ForSequenceClassification이 아닌 다른 방법은 없을까.
토론의 Q&A와 같은 방법을 사용할 수 없을까.
