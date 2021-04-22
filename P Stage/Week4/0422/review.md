## 실습1
### GPT 자연어 생성
koGPT AutoTokenizer로 load 하면 동작하지 않을 수 있어 model과 tokenizer를 수동으로 load, 사용.
 
greed search는 현재 상태에서 가장 높은 확률로만 자연어를 생성
- 똑같은 단어가 반복되는 문제

beam search는 전체 문장을 생성했을 때 문장의 확률이 최대가 되도록 생성
- 반복되는 단어들이 나오는 문제. 이를 해소하기 위해 ngram penalty

model.generate의 num_return_sequences를 통해 반환하고자 하는 sequence의 개수를 지정

사람이 만든 문장은 반드시 높은 문장의 값만 가지지 않는다. 노이즈와 랜덤을 섞어야 더 자연스럽고 항상 동일한 문장이 생성되지 않을 것이다.

=> Sampling을 이용

RandomSampling에 temperature을 추가해 높은 확률은 더 높은 확률로 선택

최종 GPT2는 Top-K Sampling을 채택해 더 자연스러운 결과를 생성

Top-p는 K 개만 바라보되 누적확률이 특정 확률 이상을 넘은 애들만 관찰을 하겠다.

### Few-shot & Zero-shot

### KoGPT-2 기반의 챗봇
Zero-shot, Few-shot은 생성할 때 앞부분에 정보를 주고 생성하게 했다면, Fine tuning은 생성 패턴 자체를 미세 조정하는 과정.

encode_batch를 해야 리스트로 만들어진 train data를 대상으로 리스트 output이 만들어진다.

bad_words_ids 등록하면 해당 토큰들이 생성되지 않도록 피하는 과정이 함수 내에서 이루어진다.

## BERT와 GPT 이후
1. XLNet
    - BERT 문제점
        + mask 토큰을 독립적으로 예측한다는 문제점.   
        + 토큰 사이의 관계 학습이 불가능. 
        + 새로운 segment에 대해서는 segment간 관계 학습 불가능
    - GPT 문제점
        + 단일 방향성으로만 학습
    위 두 문제를 보완한 방법이 XLNet
    - Relative positional encoding
    - Permutation language modeling
2. RoBERTa
    - BERT와 동일한 모델이지만 학습 시간, Bach Size, Train data 증가
    - Next sentence prediction 제거 (너무 쉬운 문제라 오히려 성능 하락)
    - Dynamic masking
3. BART
    - Transformer의 Encoder-Decoder 통합 LM
    - 다양하고 어려운 task를 한꺼번에 예측

정형화된 자연어 데이터셋이 존재하고 벤치마크가 있어야 언어에 대한 정량적 비교가 가능해진다.

4. T-5
    - Transformer Encoder-Decoder 통합 LM -> 현재의 가장 SOTA 모델
    - 학습을 할 때 마스킹 기법을 사용하지만 하나의 토큰이 아닌 의미를 가진 여러 어절을 동시에 마스킹하고, 마스크 또한 여러개의 동시에 마스킹하고 마스크도 한 번의 학습에서 다시 한꺼번에 복원
=> Transformer에 존재. multilingual 지원
5. Meena
    - 대화 모델을 위한 LM
6. Controllable LM
    - Plug and Play Language Model (PPLM)
    - 윤리성 평가 장치를 통해 발전이 필요

## 자연어 to 자연어로 충분할까?
multi-modal 연구는 필수
1. 할머니세포
2. LXMERT
3. ViLBERT
    - Bert for vision-and-language
    - BERT와 구조가 동일.
    - 이 모델은 앞에는 이미지 토큰에 대한 embedding vector를 넣고, SEP 토큰 다음에는 자연어에 대한 embedding vector를 넣어 이미지 토큰과 자연어 토큰을 하나로 합쳐 CLS 토큰을 만들어내고 이 위에 Classification layer를 부착하여 multi-modal 정보를 통해 분류를 하는 task 수행 가능
4. Dall-e
