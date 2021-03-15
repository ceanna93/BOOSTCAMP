## 1. 가벼운 모델

### 미니코드: Object in memory
python 3.6.x version 확인 후 아래 실행

print(4 != 0 not in [1, 2, 3])

print((4 != 0) not in [1, 2, 3])

print(4 != 0 not in [0, 1, 2, 3])

print((4 != 0) not in [0, 1, 2, 3])

실행 결과에 차이가 발생하는 이유는 연산자를 괄호로 묶어서 확인하거나 dis 라이브러리를 통해 확인 가능


## 동전의 뒷면
### Underspecification
모델 하나가 어떤 태스크에 딱 맞춰서 유니크하게 나오지 않는다.

전체 사이클을 알아야 한다.

edge device를 개발할 때 더더욱 필요한 시야.

model training + model evaluation 만 알아서는 시장에서 팔리지 않는다.

## 가장 적당하게
### 미니코드
euclidean / hamming / cosine distance의 차이
https://docs.scipy.org/doc/scipy/reference/spatial.distance.html

### Decision problem, optimization problem
trade-off

문제를 해결할 때 여러 Cost / 제약조건을 고려해야 한다.
