## Feature Engineering
### 강의에서 제공한 EDA(문제를 푼 횟수, 정답 추세 기타 등등)를 **전부** Feature로 추가해본다. + 05/31 Daily Mission 확인
- 한 사용자가 푼 문항의 개수
- 학생의 정답률
- 문항 별 정답률
- 시험지 별 정답률
- 태그가 얼마나 노출되었는지
- 시험지가 얼마나 노출되었는지
- 비슷한 개념을 연달아 풀면 성취도가 오를까
- 정답을 잘 맞추는 시간대

### 개인적으로 추가하고 싶은 Feature들
1. Knowledge Tag를 얼마나 많이 접했는지
2. AssessmentID를 얼마나 많이 접했는지
3. TestID를 얼마나 많이 접했는지
4. 전체 Knowledge Tag의 평균
5. 전체 AssessementID의 평균
6. TestID의 평균
7. 처음 문제를 풀었던 시간과 마지막 문제를 접한 시간

### 토론 게시판의 LGBM Feature
- 학생의 정답을 맞춘 횟수
- 학생의 문제 푼 횟수
- 학생의 정확도

### Feature의 순서를 바꿨을 때, 베이스라인과 다른 결과가 출력되는 현상을 확인하기 위해 베이스라인으로 Feature를 추가하여 모델의 성능을 확인한다.

### LSTM, Bert(Decoder)는 다른 모델에 비해 성능이 좋지 않기 때문에 앙상블을 위해서만 사용될 예정
Pseudo Labeling까지는 확인
