# 강의
## Sequence Data 문제 정의에 맞는 Transformer Architecture 설계
Transformer Models
- 아주 많은 양의 데이터와 연산량을 요구

### How to embed features for Transformers
범주형(Cetegorical)은 embedding
연속형(Continous. 숫자)은 범주형의 embedding 제외

## 대회
### Riiid
TimeSeries가 적용된 최초의 대회
### Molecular
Sequence 데이터에 Transformer가 처음 등장한 대회
Positional Embedding을 제거하면, 모든 Sequence가 서로 참조하며 제시되는 원자쌍의 순서가 반영되지 않고 학습이 가능
### MoA
1. Sequence로 묶을 수 있는 데이터가 없다
2. Feature는 많다
3. 데이터는 적다
=> Transformers를 적용했을 때 성능이 나오지 않았다.

1D CNN + Feature Ordering

Text CNN

### 질문
1. 숫자를 일정 범위로 나눠 학습시킬 때 효과
2. RNN + Teacher Forcing과 단순 RNN 차이
3. K-Fold의 값에 차이가 많이 나는 이유
4. 데이터가 많아야 Transformer의 효과가 난다고 하는데 데이터는 학습 데이터가 맞는지.
