# BERT 언어모델 기반의 단일 문장 분류
### 1. KLUE 데이터셋
한국어 자연어 이해 벤치마크(Korean Language Understanding Evaluation, KLUE)

살면서 직면하게 되는 거의 모든 자연어 task 유형

- 문장 분류
- 관계 추출
- 문장 유사도
	- 챗봇. 코사인 유사도를 통한 두 문장의 유사도 계산
- 자연어 추론
	- 두 문장 관계 분류 task
- 개체명 인식
- 품사 태깅
- 질의 응답
	- 위 세 개는 문장 토큰 분류 task
- 목적형 대화
	- DST
- 의존 구문 분석

## 의존 구문 분석
단어들 사이의 관계를 분석하는 task

의존소 / 지배소
- 의존소 : 지배소가 갖는 의미를 보완해주는 요소(수식)
- 지배소: 의미의 중심이 되는 요소

충무공 이순신을 조선 중기의 무신이다.
지배소: 이순신
의존소: 충무공

의존 구문 분석
- 복잡한 자연어 형태를 그래프로 구조화해서 표현 가능. 각 대상에 대한 정보 추출이 가능

## 단일 문장 분류 task
주어진 문장이 어떤 종류의 범주에 속하는지를 구분하는 task


# 개인 공부
### Competition
성능 향상 시도 가능 방법
1. Multi Sentence에서 \[SEP\] 토큰을 제거하여 Single sentence로 변경하여 학습
2. Tokenizer를 변경
3. [Kakao의 pororo](https://github.com/kakaobrain/pororo)를 이용한 Data augmentation
4. Trainer의 Loss 변경
	- 방법은 Trainer 객체 상속 후 compute_loss 메서드를 오버라이딩
5. AutoModel 사용
	- [AutoModel](https://huggingface.co/transformers/v3.0.2/model_doc/auto.html), AutoConfig 파악 필요
6. ~~Tokenizer의 max_length변경~~
	- Bert에서 300으로 변경 후 시도 시 Accuracy 하락
	- 분포에서 가장 많은 값보다 적당한 값 탐색 필요
7. entity embedding 추가
8. Soft label
	- task가 어려울수록 학습이 잘 된다.
