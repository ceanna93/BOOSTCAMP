### 인코더와 디코더

### 임베딩

### Cross Entropy (손실 함수)

### Normalization과 Regularization
둘 다 정규화라고 불림

**Normalization**

- 데이터를 조정
- 학습 전에 scaling 하는 것
  - 머신러닝에서 scale이 큰 feature의 영향이 비대해지는 것을 방지
	- 딥러닝에서 Local Minima에 빠질 위험 감소(학습 속도 향상)
- 값의 범위(scale)를 0~1 사이의 값으로 바꾸는 것

**Regularization**
- weight를 조정하는데 규제(제약)를 거는 기법
- Overfitting을 막기위해 사용함
- Generalization 성능을 높이는데 도움
- L1 regularization, L2 regularizaion, Dropout, Early Stopping 등의 기법이 있음

https://light-tree.tistory.com/125

https://realblack0.github.io/2020/03/29/normalization-standardization-regularization.html
