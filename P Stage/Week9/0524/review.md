# 강의
## DKT Task 이해
Deep Knowledge Tracing

딥러닝을 이용해서 지식 상태 추적

Knowledge Tracnig
- 지식 구성 요소: 학생에게서 알고 싶은 지식
- 지식 상태: 각 지식에 대한 학생의 이해도
지식 상태는 계속 변화한다. => 변화하는 지식상태를 지속적으로 추적

시험지: 문제 풀이 정보 => 예측한 지식 상태

문제 풀이 정보가 추가될수록 학생의 지식 상태를 더 정확하게 예측할 수 있다.

데이터가 적을수록 오버피팅 현상이 쉽게 일어난다.

훈련이 끝나면 지식 상태를 예측할 수 있다. DKT를 통해 학생이 얼마나 아는지를 측정할 수 있다.

### DKT 활용
문제 추천, 학업도 파악

### DKT 대회
binary classification 문제

주어진 문제를 맞췄는지에 집중한다.

다양한 Feature가 존재

## Metric 이해
Model의 예측은 0~1 사이의 값
### Confusion Matrix
- F1 Score = 2 * (Recall * Precision) / (Recall + Precision)
- Recall과 Precision은 반대. Recall은 더 많은 값을 True라고 예측하면 오르고, Precision은 1을 더 정확하게 맞춰야 오른다.
- Recall은 실제 True 중에 모델이 True이라고 예측한 값의 비율, Precision은 모델이 예측한 True 중 모델이 True를 맞춘 비율

### AUC(Area Under the roc Curve) => 분포 Metric
면적이 넓을수록 모형 성능이 높아진다.

AUC가 이상적인 이유
- 척도 불변. 절대값이 아니라 예측이 얼마나 잘 평가되는지 측정. 0과 1의 분포의 차이가 중요
- 분류 임계값 불변.

척도 불변/분류 임계값 불변이 항상 이상적이진 않다.

## DKT Trend
DKT는 Sequence Data

### Sequence 모델
RNN/LSTM/SEQ2SEQ/ATTENTION/TRANSFORMER

## DKT Data Exploratory Data Analysis
EDA를 할 때 기술 통계량을 보게 된다.
Data Frame -> Column

Scheme(Feature) -> **numeric/discrete**을 나누고 이에 따라 EDA와 Preprocessing, input이 달라질 수 있다.

# Competition
EDA
