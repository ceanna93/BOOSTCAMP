## 02/15 Peer Session

### 1
  - **Q.** Word2Vec에서 windows의 크기는 개발자가 임의로 결정해도 되는지. 권장되는 크기가 있는지.
  - **A.** Word2Vec과 관련된 논문에서 Window 크기와 관련된 언급이 없었다. 정확한 크기가 결정된 것은 없는 것으로 생각됨

### 2
  - **Q.** Word2Vec과 GloVe 중 어느 쪽이 성능이 더 좋은지.
  - **A.** 실제로 성능은 비슷하며 큰 차이를 느끼지 못했다는 경험담. word embedding에 따른 결과를 보고 더 성능이 좋은 걸 택하는 것을 추천.

### 3
  - **Q.** Word2Vec과 GloVe을 이용한 NLP에서 신조어/문법 파괴 문장에 대한 처리는 어떻게 가능할지. 전처리를 이용해 일반적인 문장으로 변경해야 할 지, 이모티콘 처리는 어렵지 않을지.
  - **A.** 전처리 후 generalization된 문장을 사용하는 방법과 전처리를 하지 않는 방법으로 NLP process를 진행했을 때, 전처리를 하지 않는 편이 더 높은 성능을 보였다는 문재훈님의 경험담. 주의가 필요한 문장들을 처리해야 하는 경우 stopword 설정에 조금 더 주의를 두고 진행해야 한다는 결론.

### 4
  - **Q.** Sentiment analysis에서 반어법 처리도 가능할지.
  - **A.** 문재훈님이 실제로 영화 평점 리뷰 데이터를 이용하여 비꼬는 표현과 반어법 사용한 경우를 구분하려 했으나 앞뒤 문맥 없이 짧은 글에서 판단하기 어려움이 있었다는 설명. 실제로 영화를 본 적 없는 사람도 하나의 리뷰만 단독으로 봤을 때 해당 리뷰가 긍정적인 반응인지, 비꼬는 반응인지 구분하기 어렵다고 생각.