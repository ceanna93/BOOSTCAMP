## 두 문장 관계 분류
주어진 2개의 문장에 대해, 두 문장의 자연어 추론과 의미론적인 유사성을 측정하는 task
CLS 토큰 위에 classificatiion layer를 부착시켜 두 문장의 관계를 분류

### 두 문장 관계 분류를 위한 데이터
- Natural Language Inference (NLI)
- Semantic text pair

## 두 문장 관계 분류 모델 학습
Information Retrieval Question and Answering (IRQA)

## 실습
가장 뒷단에 paraphrase detection 모델을 부착. 유사한 Top N 개를 이진 분류를 통해 유사한지 아닌지 판단.
