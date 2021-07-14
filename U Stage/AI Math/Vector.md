# 벡터가 뭔가요?
숫자를 원소로 가지는 리스트(list) 또는 배열(array)
- 공간에서의 한 점을 나타낸다. (n차원 공간에서의 한 점)
- 원점으로부터 상대적 위치
- 숫자를 곱해주면 길이만 변한다. αx에서 α를 스칼라(Scala: 0차원 텐서의 다른 표현)라 부르며 벡터에는 스칼라곱이 가능하다.
    - α가 0보다 작으면 반대방향
- 벡터끼리 같은 모양을 가지면 덧셈, 뺄셈을 계산할 수 있다.
- 벡터끼리 같은 모양을 가지면 성분곱(Hadamard product/element wise produce)을 계산할 수 있다.
- 두 벡터의 덧셈은 다른 벡터로부터 상대적 위치 이동을 표현
- 벡터의 노름(norm)은 원점으로부터의 거리

## 노름(Norm)은 뭔가요?
- L1 norm: 각 성분의 변화량의 절대값을 모두 더함
    - Robust 학습, Lasso 회귀
- L2 norm: 피타고라스 정리를 이용해 유클리드 거리를 계산
    - Laplace 근사, Ridge 회귀
    - np.linalg.norm
- 노름의 종류에 따라 기하학적 성질이 달라진다.
- 기계 학습(머신러닝)의 목적 ,필요에 따라 다르게 사용

## 두 벡터 사이의 거리
L1, L2 노름을 이용하여 두 벡터 사이의 거리를 계산
- 벡터의 뺄셈을 이용
- |y-x| = |x-y|

## 두 벡터 사이의 각도
L2 노름에서만 각도 계산이 가능
- 제2 코사인 법칙에 의해 두 벡터 사이의 각도를 계산
- 분자를 쉽게 계산하는 방법이 내적(inner product)
    - np.inner

## 내적
정사영(orthogonal projection)된 벡터의 길이와 관련
- 내적은 정사영의 길이를 벡터 y의 길이 |y|만큼 조정한 값
- 내적은 두 벡터의 유사도(similarity)를 측정하는데 사용 가능