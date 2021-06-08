# 강의 
## 데이터 관련 직군
Data Science는 Deploy에 관여를 안 하고 있지만 Machine Learning Engineer는 Deployment에 관여

## 모델 서빙
### On-devie Serving(Edge Device)
경량화를 통해 스마트폰과 같은 장비에서 추론

디바이스 내에서 [입력]-[추론]-[출력] 과정을 처리

### Cloud-based Serving
복잡한 추론

서버로 입력을 전달해 [추론]만 서버에서 처리하고 [출력]을 디바이스로 전송

서버의 end point 필요

## 웹 서버를 활용한 모델 서빙
### HTTP 통신
HTTP(HyperText Trasnfer Protocol) 통신: 가장 범용적으로 사용되는 네트워크 통신 방법

클라이언트와 서버 사이의 요청-응답 프로토콜

Uniform Resource Locators(URLs)

### 웹 서버 구축
#### Flask
독립적인 서버로 구성하는 것을 권장(웹 서비스와 머신러닝 모델을 서빙하기 위한 하드웨어 자원이 다름)

## MLflow를 활용한 모델 서빙
머신러닝 라이프 사이클을 관리할 수 있는 툴을 활용한 서빙
- MLflow Tracking
		- 실험 관리
- MLflow Projects
- MLflow Models
		- API 현태로 모델을 서빙

