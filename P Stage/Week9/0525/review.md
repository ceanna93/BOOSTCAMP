# 강의

# Competition
### 의문
1. timestamp와, id와 같은 feature를 간단한 값으로 바꿨을 때의 효과. => 캐글의 타이타닉 preprocessing을 보면 연령을 범위로 변경하여 학습한다.
    - https://www.kaggle.com/gunesevitan/riiid-answer-correctness-prediction-eda
2. 데이터는 단순하고 어려운 Task일수록 모델의 성능이 좋아지는 건지.
3. 같은 문제를 얼마나 많은 사람들이 풀었는지에 대한 정보가 학생 A의 점수 예측에 도움이 될지.
4. 예전에 풀었던 유사한 유형의 문제를 풀었을 때 문제의 정답 여부와 경과 시간(log), 유사한 유형에 대한 추세를 학습
5. 접근 방법.
    - 전체 데이터를 넣고 1/0을 출력하는 방법(Many-to-One)
    - Sequential하게 예측하여 가장 마지막에 1/0을 예측하는 방법(Many-to-Many)

### 참고
+ [Correctness prediction paper](https://arxiv.org/abs/2010.12042)
+ [Attention Mechanism](https://arxiv.org/pdf/2102.04250.pdf)
