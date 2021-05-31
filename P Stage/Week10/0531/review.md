# 강의
Kaggle Riiid Competition Winner's Solution
## Feature Engineering
### Top-Down
- Data-driven
- ML Approach
		1. EDA를 하면서 이상한 부분 탐색
		2. CV로 성능이 향상되는 것을 검증하고 제출
### Top-Down
- 가설 기반
- 가설 - 구현 - 검증

### 숫자형
- Null 값 확인
- min, max, 1Q, median, 3Q, range
- mean, std

### 범주형
- 최빈도 값
- Value별

### 공통
- 파일크기
- 컬럼수, 로우수
- 중복로우

- 변수 간 상관 관계

### 사용자 별 문항 푸는 패턴
- 문항의 정답을 하나로 찍는 경우
		- Riiid에서는 맞았는지 틀렸는지만 존재하기 때문에 적용이 불가능
- 사용자가 문항을 푸는 데 걸린 평균 시간보다 오래 걸렸을 경우
		- 실력이나 다른 요인에 의하여 문제 푸는 데 걸리는 시간이 달라질 수 있음
		- 해당 문항을 맞춘 학생의 평균 시간과 틀린 학생의 평균 시간 2가지를 Feature로 주어 활용

- 사용자 정답률 추이
- 이전에 풀었던 문항/시험지가 다시 등장하는 경우

### 문항 별 특징
직접적인 정보
- 문항의 정답률
- 문항이 가진 태그의 정답률
간접적 특징
- 문항-태그 정보로 content2vec
- 사용자-문항 정보로 SVD, LDA, item2vec
- 문항을 특징화하는 IRT, ELO

- 문항, 시험지, 태그의 평균 정답률
- 문항, 시험지, 태그의 빈도

### Data Leakage
- train data에서 뽑은 정답률이 test에서도 반드시 정답률이 일치한다고 확신할 수 없다.

CV와 Public 에서 점수가 오르면 overfitting이 적다.

### 다양한 방법을 통한 문항 고유의 Feature를 뽑아내기
- 문제의 난이도 이론인 ELO, IRT를 활용
- 학생과 문항 별로 고유한 특성이 있다는 가정
- 만약 학생의 잠재 능력을 알고, 문항 별로 모수를 안다면 전체 학생의 모든 문제를 맞출 확률을 모두 알 수 있다.

### 시간 데이터 임베딩
Continuous Embedding
- 시간과 같은 연속형 데이터를 새로운 방법으로 임베딩
		- 임베딩 행렬을 사용하는 대신 주어진 연속형 데이터 값에 가중을 더 두고 그 주변 값들에 더작은 가중을 주어 이 임베딩 행렬의 특정 열들을 가중합한 벡터를 임베딩으로 사용

## Riiid Winner's Solution - Last Query Transformer RNN
1. LGBM, DNN
- **아주 많은 Feature를 만들어내**야 하고, 유의미한 것을 찾기도 어려움
2. Transformer
- 아주 많은 양의 데이터를 요구로 하고, **sequence 길이의 제곱에 비례한 시간 복잡도**를 가지기 때문에 사용하기에 부담스러움

두 가지 문제를 모두 해결한 방법
1. 기본적인 Feature만 사용하고 seq를 증가
2. 마지막 Query만 사용하여 시간 복잡도를 낮춤
3. Transformer는 position에 대한 정보를 없애고 Feature Extraction에만 사용되도록 사용
		- 일련의 Sequence 사이 특징들을 LSTM을 활용해 뽑아낸 뒤 마지막에 DNN을 통해 Sequence 별 정답을 예측함
		- 문제간 특징을 Transformer로 파악하고 일련의 Sequence 사이 특징들을 LSTM을 활용해 뽑아낸 뒤 마지막에 DNN을 통해 Sequence 별 정답을 예측

## Why Kaggle
Top-Down 방식으로 AI를 이해할 수 있다!

# Competition
Transformer에서 query의 크기를 1로 설정
