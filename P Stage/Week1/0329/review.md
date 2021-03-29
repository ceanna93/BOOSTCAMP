## Competition with AI Stages!

### P Stage
- 머신러닝 파이프라인의 한 부분을 경험
- U Stage에서 경험한 이론을 바탕으로 실제 데이터와 코드베이스를 통한 이해
- Competition 형태의 실습을 통해 점진적인 모델 성능 향상을 경험
- 전체적인 프로세스 경험

### Competition
주어진 데이터를 이용해 원하는 결과를 만들기 위한 가장 좋은 방법

#### Overview
**방향성**
- 의사 결정에 도움이 된다.
- 어떤 대회인지 알아야 한다.
- 대회의 Overview를 분석하고 중요한 정보들을 확인한다

##### 숙제
Problem Definition (문제 정의)
- 내가 지금 풀어야 할 문제가 무엇인가
- 이 문제의 Input과 Output은 무엇인가
- 이 솔루션은 어디서 어떻게 사용되어지는가 (일반화, 사용 범위는 어디까지인가)

#### Data Description
File 형태, Metadata field 소개 및 설명

#### Notebook
Notebook을 제공하는 대회
aistages를 통해 좋은 성능에서 train이 가능

#### Discussion
등수를 올리는 것보다, 문제를 해결하고 싶은 마음
마지막 2주 전부터는 중요한 정보를 공유하지 않지만 그 전까지는 정보를 공유한다.

### 왜 Competition
- Machine Learning Flow, 전체적인 파이프라인에 대해 경험
- 도메인 이해를 먼저 한 다음 데이터 분석

## Image Classification & EDA
### EDA
Exploratory Data Analysis
- 데이터를 이해하기 위한 노력

#### EDA의 진짜 목적
데이터를 이해하기 위해 **궁금한 것**을 확인하는 것

방법(도구)은 여러가지가 있을 수 있다. 반드시 캐글의 Notebook에서 많이 사용하는 방법을 사용하지 않아도 된다.

호기심들을 명제로 나열하는 작업이 도움이 된다.

이후 코드로 구현하는 과정

### Image Classification
#### Image
시각적인 인식을 표현한 인공물(Artifact)

#### Model
Input + Model = Output


## Competition EDA
+ 연령 분포 확인
<img src="https://user-images.githubusercontent.com/12611645/112861072-6de15700-90ef-11eb-9821-136a7a9f4934.jpg" width="60%" height="50%" title="Age distribution" alt="NLPDiagram">

+ 성별 분포 확인

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data["gender"].value_counts()

<br />

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;female    1658

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;male      1042

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Name: gender, dtype: int64

<br />

+ 연령 분류 후 분포 확인

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data.loc[ data['age'] < 30, 'age'] = 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data.loc[(data['age'] >= 30) & (data['age'] < 60), 'age'] = 1

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data.loc[ data['age'] >= 60, 'age'] = 2

<br />

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0    1281

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1    1227

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2     192
