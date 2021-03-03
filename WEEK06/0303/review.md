## 캐글 그랜드마스터의 경진대회 노하우 대방출
캐글을 어떻게 사용해야 더 효과적인지. 왜 캐글에 도전해야 하고 캐글에 도전하면 좋은 점에 대해 배웠습니다. 마스터 세션을 통해 캐글에 처음 도전하는 사람에 대한 조언을 많이 받을 수 있었습니다. 그 외에 취업과 관련하여 현실적인 조언을 들을 수 있는 기회였습니다. P 스테이지에서 열심히 해야겠다고 생각했습니다.

## Fullstack Machine learning Engineer
Fullstack과 ML을 병행할 때의 어려움을 간접적으로 알 수 있었습니다. 원래 Backend에 관심이 있었는데 마스터세션을 통해 발등에 불이 떨어진 느낌으로 서둘러 ML 공부와 함께 web도 구현해봐야겠다고 생각하게 되었습니다. 웹 개발이 처음이라면 어떻게라도 완료하는 것을 목적으로 '잘'하는 것보다 '빨리'가 중요하다는 사실을 배웠습니다.

### Normalization과 Regularization
**Normalization**
- Data scaling
- https://goodtogreate.tistory.com/entry/Neural-Network-%EC%A0%81%EC%9A%A9-%EC%A0%84%EC%97%90-Input-data%EB%A5%BC-Normalize-%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0
- https://eunsukim.me/posts/understanding-normalization
- Z-score normalization = standardization
- https://goodtogreate.tistory.com/entry/Neural-Network-%EC%A0%81%EC%9A%A9-%EC%A0%84%EC%97%90-Input-data%EB%A5%BC-Normalize-%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0
- 입력변수가 MLP에서와 같이 선형적으로 결합된다면 적어도 이론 상으로는 입력을 표준화하는 것이 거의 필요하지 않음
- 그 이유는 해당 weight와 bais를 변경하여 입력 벡터를 재조정하면 이전과 완전히 똑같은 결과를 남길 수 있기 때문. 그러나 입력을 Standardization하면 학습을 더 빨리하고 지역 최적의 상태에 빠지게 될 가능성을 줄이는 다양한 실용적인 이유가 있음. 또한, 표준화 된 입력을 통해 Gradient Descent 및 Bayesian estimation을 보다 편리하게 수행할 수 있음

출처: https://goodtogreate.tistory.com/entry/Neural-Network-적용-전에-Input-data를-Normalize-해야-하는-이유 [GOOD to GREAT]

**Regularization**
- overfitting 방지
