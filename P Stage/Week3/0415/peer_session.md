Q. 피씨방에서 mecab으로 분리했을 때 피, 씨방으로 분리되면서 씨방이 욕설로 처리되는 경우가 있음. 이를 해결하기 위한 방법은 무엇이 있을까?

A. 과하게 욕설을 필터링한 결과라고 생각. 잘못된 결과는 아니라고 생각한다는 의견.

Q. 서버 메모리가 없을 때 비워야 하는 대상

A. checkpoint.
checkpoint로 저장한 모델이 3개밖에 되지 않는데 메모리를 전부 사용한 이유. 메모리를 2인 당 1개로 할당하기 때문에 다른 사람이 많이 사용하고 있으면 할당이 되지 않을 수 있다.

position_embedding_type="absolute"
absolute를 변경하면 상대 경로로 사용 가능

베이스라인 코드에서 pretrained된 모델을 사용하고 있지 않기 때문에 코드를 수정해줘야 한다.

BERT에서 CLS 토큰을 이용하는 게 반드시 성능이 좋지는 않을 수 있다.
- https://stackoverflow.com/questions/62705268/why-bert-transformer-uses-cls-token-for-classification-instead-of-average-over
- https://stackoverflow.com/questions/60087613/why-take-the-first-hidden-state-for-sequence-classification-distilbertforsequen

#### Augmentation 방법
- 번역을 두 번 해서 한국어로 다시 번역된 데이터를 데이터에 추가
- 다른 나라 말로 번역해서 해당 언어로 학습하는 방법
- 영어로 학습하기
- 엔티티를 바꿨을 때 의미가 유지되는 경우를 찾기
