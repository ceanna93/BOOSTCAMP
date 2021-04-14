## BERT 언어모델
Seq2Seq, Attention + Seq2Seq, Transformer
이미지 Autoencoder 압축된 형태로 표현
Decoder의 목적은 원본을 복원
Autoencoder network에서 Compressed 된 Neural network의 vector정보를 가지고 오면 입력된 이미지에 대한 vector 값이 될 수 있다. 본인 스스로를 가장 잘 표현할 수 있게 학습된 모델

### BERT
NLP 실험
- 단일 문장 분류
	- 하나의 문장이 입력됐을 때 이 문장이 어떤 클래스에 속하는지 분류
	+ 감성 분석
	+ 관계 추출
- 두 문장 관계 분류
	- 두 문장의 관계를 분류
	+ 의미 비교 (문제는 유사도가 없는 문장으로 학습한 모델은 사용이 불가능, 유사도가 있는 문장으로 학습해야 한다.)
- 문장 토큰 분류 (개체명 인식기)
	- CLS 토큰이 입력된 문장의 정보가 녹아있다고 하는데 각 토큰의 출력에 분류기로 부착
	+ 개체명 분석
- 기계 독해 정답 분류
	- 2가지 정보가 주어진다. (질문, 정답이 포함된 문서) 문서 내 토큰이 굉장이 많은데 이 토큰 내에서 정답(start point, end point)이 어디인지 잡아내는 것.
	+ 기계 독해
	+ Task에 맞춰 Tokenizing을 정의
	+ 어절 단위 tokenizing에서 음절 단위 tokenizing을 했을 때 점수가 향상되는 이유. (조사가 붙지 않은 단어 추출 가능)

### 한국어 BERT
- ETRI KoBERT
	- 형태소 단위로 분리하고 WordPiece
	- 의미를 가지는 최소 단위로 분리하고 WordPiece를 적용
	- ETRI 형태소 분석기를 사용해야 한다.
- 형태소 분석을 먼저 하는 게 가장 성능이 좋았다.

### Advanced BERT model
- 원본 문장
- Entity 후보 추출
- 주요 entity 추출
- 전처리 (**entity embedding**을 추가했을 때 적은 학습 데이터로도 BERT의 성능 향상)

### 실습
- BertTokenizer
- tokenize() option: add_special_tokens, max_length, truncation, padding(문장의 앞, 뒤 또는 segment를 채울 수 있다)
- decode()

UNK가 많을 수록 원본 문장의 의미가 사라진다.
에어비엔비에 맞는 vocab을 추가한다.
- add_tokens()
- add_special_tokens 토큰 추가 additional_special_tokens
- pipeline()

transformers의 장점은 pipeline을 이용하여 쉽게 inference 가능

Cosine similarity가 높다고 하더라도 의미론적으로 유사하지 않을 수 있다.

### BERT를 이용한 Chatbot 만들기
문제.
1. 데이터가 너무 적다. 동문서답
2. 감정 분석이 불가능하다.
