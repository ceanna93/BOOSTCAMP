# 강의
## Real World
- Understanding of business problem
- Problem formalization
- Choice of target metric
- Deployment issue
- Inference speed
- Data collecting
- Model complexity
- Evaluate model in real world

Real World와 Competition이 차이점이 발생하는 지점은 Target metric value

대회는 소수점 경쟁으로 운이 많이 작용한다고 볼 수도 있지만 소수점을 증가시키기 위해 다양한 방법을 적용하는 것 자체가 의미가 있는 것 같다.

## Commercial success
- Supervised learning
- Transfer learning

### Filed 문제 유형
Classical Mashine Learning -> Supervised -> Classification -> Binary-class -> Imbalanced(가장 많은 유형)

## 문제 정의 3요소
1. Input (Data_X, Data Type)
		- 데이터 유형
		- 데이터 건수
		- 데이터 용량
2. Output (Data_Y, 예측해야 할 값)
		- Label 여부
		- 1차 Task 여부
		- Classification 일 경우 Output Class 별 비율
3. Metric (평가지표)
		- 모델 성능
		- KPI(Key Performance Indicator, 핵심성과지표: 실제 사업에 적용해서 어떤 성과를 내는지, offline과 online의 성능 차이가 많이 날 수 있음)

4. Input + Output (Data)
		- 최종 Task 결정
		- Model Architecture

## Workflow
### 작업의 흐름
범용적인 의미: 특정 비즈니스 결과를 달성하는 상호 의존적인 프로세스 및 작업 그룹

### 언제 필요할까?
- ETL pipelines
- Machine Learning Pipelines
- Predictive Data Pipelines
- General Job Scheduling

## Machine Learning Workflow
시스템 관점에서 고민해봐야 할 것들
1. 데이터 수집
		- 얼마나 많은 데이터?
		- 데이터의 Source가 여러개?
		- 한번만 수집하면 되는지? 주기적으로 수집해야 하는지?
2. 데이터 전처리
		- 데이터들이 모두 같은 포맷을 갖는지?
		- 단일 머신에서 처리 가능한지
3. 모델 훈련
		- 모델 훈련을 병렬적으로 할 건지?
		- 데이터 기반으로 업데이터가 되어야 하는지, 성능 기반으로 업데이트가 되어야 하는지
4. 배포
		- 사용자가 증가할 수 있는지
		- Downtime이 존재할 수 있는지(업데이트 중에는 접속이 불가해도 되는지)
5. 전체 프로세스
		- 이전 작업들이 모두 순차적으로 이루어져야 하는지, 부분적으로 이루어질 수 있는지
		- 모든 작업들이 주기적으로 이루어지는지

## Apache Airflow
A workflow management system
### 구성요소
- Webserver
- Scheduler
- Worker
- Meta DB

### DAG(Directed Acyclic Graph)

## ML 적용을 두려워하지 말라
Biggest Gain in ML is First Launch

## Technically vs Economically
Enonomically Feasible과 Technically Feasible의 만나는 범위를 늘려야 한다.
