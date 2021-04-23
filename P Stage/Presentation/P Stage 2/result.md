# Wrap up report
## 기술적인 도전
### I. 일정
<img src="https://user-images.githubusercontent.com/12611645/115821802-6e46e680-a43e-11eb-9100-992b9d94fb7c.JPG">

### II. 각 작업
1. EDA
    - 토론 게시판과 데이터 중복을 확인
    - 데이터 중복 제거 전처리로 성능 향상 확인
2. Augmentation
    + Label 변경으로 Augmentation 시도
    + 토론 게시판의 데이터셋 사용
    + 토론 게시판의 pororo를 이용한 번역으로 Augmentation 시도
3. Model
    - Hyperparameter optimization
    - koelectra-base-v3-discriminator
    - roberta-large
    - xlm-roberta-large
4. Tokenizer
    - Typed entity marker
        - Special token 추가
        - 특수 문자 추가
    - KoBertTokenizer
    - entity 사이 token 변경
        - 토큰 제거(공백)
        - 토큰 변경(Special token)
5. Hyperparameter optimization
    - 토론 게시판의 하이퍼파라미터
    - seed 값 변경
    -	Seed: 2020

**최초 Hyperparameter**
|Hyperparameter|값|
|:---|:---:|
|Seed|2020|
|Epoch|5|
|Batch size|16|
|Learning rate|5e-5|
|Weight decay|0.01|
|Warmup steps|500|

**최종 Hyperparameter**
|Hyperparameter|값|
|:---|:---:|
|Seed|142|
|Epoch|10|
|Batch size|32|
|Learning rate|1e-5|
|Weight decay|0.01|
|Warmup steps|300|

6. Ensemble
    - Soft Ensemble
    - Weighted Ensemble

### III. Accuracy 변화
<img src="https://user-images.githubusercontent.com/12611645/115822186-165caf80-a43f-11eb-811f-0abdb75c6bca.JPG">
- 붉은선: xlm-roberta-large 사용
- 녹색선: 앙상블

### 아쉬웠던 점
- xlm-roberta-large를 적용한 시점부터 시간이 부족해 코드가 많이 지저분해졌다.
- ner을 이용하여 inference 부분에서 filtering을 추가해보고 싶었지만 시간이 부족했다.
