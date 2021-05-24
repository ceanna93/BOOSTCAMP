# 수업개요

### 강의 소개

본 강의는 DKT 태스크 소개와 DKT를 풀기 위한 시퀀스 데이터 모델링에 대해 배우고, 그 중 가장 핵심적인 아키텍쳐인 Transformer를 NLP 이외 도메인에 활용하는 방법을 다룹니다.
현장에서 Project 수행시 겪는 여러 Hurdle, Challenge 에 대해 이해하고, Model Serving 등 End-to-End Project 수행 연습을 통해 실제 Project 수행 능력을 함양합니다

### 강의 목표

- DKT 태스크에 대한 이해 및 여러 접근방법과 장단점 파악
- Transaction Data등 Sequence Data Model 이해 및 구현
- 문제에 맞는 Transformer Architect 설계 및 구현
- End-to-End Project 수행 연습

### 강의 타겟

- Python, Pytorch를 어느 정도 다룰 줄 아는 수강생
- DKT 등 교육 AI에 관심 있는 수강생
- Sequence Data Modeling에 관심 있는 수강생
# [5/24 월] Intro & EDA

### 1강 DKT 이해 및 Sequence Data Modeling
- DKT task 이해
- DKT History 및 Trend
- metric
- Sequence Data Modeling
    - LSTM
    - Transformer
### 2강 DKT data EDA
- i-Scream 데이터 소개
- i-Scream 데이터 EDA
# [5/25 화] 

### 3강 Baseline (LGBM, LSTM, Transformer)
- LGBM
- LSTM + attention
- Transformer
# [5/26 수] 

### 4강 Sequence Data 문제 정의에 맞는 Transformer Architecture 설계4. 
- Competition
    - Molecule Prediction
    - Data Science Bowl 2019
    - Riiid
    - MoA
- Architecture
    - Transformer Enc
    - Transformer Enc + Dec
# [5/27 목] 

### 5강 Transformer Input Representation, Output 구현
- Input Representation 구현
- Outptut 구현 
# [5/28 금]

### Office Hour - 조대현 멘토
- Baseline 톺아보기
# [5/31 월] 

### 6강 Kaggle Riiid Competition Winner's Solution 탐색
- 성능 개선을 위한 Kaggle Solution 및 idea 벤치마크
- Kaggle Approach
# [6/1 화]

### 7강 Model 성능 개선
- Transformer Tuning
- LGBM, LSTM
# [6/4 금]

### Office Hour - 박현병 멘토
- DKT 논문 톺아보기
# [6/7 월] 

### 8강 ML Pipeline
모델링 Pipeline 전반 소개
# [6/8 화]

### 9강 Model Serving 
- 이론
- 웹서버 기본적인 내용 HTTP 통신
- Serving Architecture 설명
- 실습
- 도커 환경 설정
- Flask를 활용한 서빙
- MLflow를 활용한 서빙
# [6/9 수] 

### 10강 End-to-End 프로젝트 수행
- 이론
- ML 파이프라인 구성시 고려해야할 요소 (아키텍쳐적인 관점)
- 실습
- Airflow를 활용한 ML 파이프라인 조율
- Offline Train 과 Online Serving 사이의 Configuration 전달
- 데이터 수집 부터 서빙까지의 과정을 시뮬레이션 해 볼 수 있도록 과제 구성
- 웹어플리케이션에 모델 서빙 연동하여 실서비스 유사경험
# [6/10 목]

### Office Hour - 서중원 멘토
- P stage에서 진행한 모델들에 클라이언트 사이드를 적용한 배포 과정 소개
# [6/16 수] 

### 마스터 클래스
- Competition Wrap-up
- 1st, 2nd, 3rd Placeholder 캠퍼분들 방법 발표
