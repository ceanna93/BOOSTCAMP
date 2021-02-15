## Intro to NLP
[Intro to Natural Language Processing](https://ceanna93.github.io/ai/intro-to-nlp/)

## Bag of words
Bag-of-words
+ Step 1. Constructing the vocabulary containing unique words
+ Step 2. Encoding unique words to one-hot vectors
 해당 dimension의 값만 1
 one-hot은 word embadding 기법과 대비되는 특성
 단어의 의미가 관계 없이 모든 단어가 동일한 관계를 가진 형태로 단어의 벡터 표현 설정

Bayes' Rule
P(d|c)
특정 카테고리 c가 고정되었을 때 문서 d가 나타날 확률
문서 d는 w1부터 wn까지 동시에 나타나는 동시 사건
각 단어가 등장할 확률: c가 고정된 경우 서로 독립이라고 가정할 수 있다면 P(Wi|c)로 표현 가능

NaiveBayes는 클래스가 3개 이상일 때도 사용 가능
단어가 존재하지 않으면 확률이 0이 되어 절대 해당 클래스로 분류되지 않는다.
=> regularization 필요

단어가 나타나는 확률 값, 파라미터 추정 방식은 mle 수식을 통해 유도
 -> 관련 자료 찾기

regularization 관련 내용

## Word Embedding
word2vec
한 단어가 주변에 등장하는 단어를 통해 의미를 알 수 있다.
확률분포 예측
P(w|"cat")
주변 단어를 숨긴 채 word2vec 학습
sliding window

GloVE 차이점
각 입력 및 출력 단어 쌍들에 대해서 학습 데이터에 두 단어가 한 윈도우 내에서 몇 번 동시에 등장했는지 사전에 미리 계산하고 입력어들의 embedding vector(내적값)이 최대한 fitting될 수 있도록 내적 값 사용

word2vec의 경우 빈번하게 자주 등장하는 경우 여러번에 거쳐 학습되므로 word embedding 내적값이 그에 비례해서 커지도록 한다.
GloVe에서는 동시에 등장하는 횟수를 미리 계산하고 이에 대한 log를 취한 값을 두 단어 간의 내적값의 ground truth로 사용하여 학습 진행
중복 계산을 줄인다는 장점
학습이 상대적으로 더 빠르게 진행되고 보다 적은 데이터에 대해 잘 동작함
선형대수의 관점에서 추천 시스템에서 많이 활용되는 알고리즘의 task로도 이해

