## 행렬 분해
미니코드: Approximation

### Three maps
Matrix is a data modeling tool

Matrix
- 이차원
Tensor
- 삼차원 이상을 표현

#### 3원 1차 연립방정식을 행렬로 표현할 수 있다.

### Gaussian elimination
Matrix의 rank를 계산

#### Terminology
2. 두 벡터가 겹치면 이 차원을 결정할 수 없기 때문에 independent

Matrix dimension = rank + nullity

#### Filter와 Kernel의 차이
kernel이라는 것은 sliding window 하는 영역에서의 크기이다.

filter라는 것은 실제로 kernel이 weighted sum 하는 영역의 크기이다.

https://data-science-hi.tistory.com/128

### Kernel method
#### Kernel is an umbrella term

#### filter decompose

### Matrix decomposition
neural network 이전에 추천 시스템에서 matrix의 approximately 사용

#### Eigenvalue Decomposition
Eigen vector

Matrix linear transformation

원점을 변환시켰을 때 vector가 길이만 바뀌게 되는 vector를 eigen vector라고 한다. Matrix를 변형시켰을 때도 벡터의 방향이 보존될 때 변하는 양을 Eigenvalue라고 부른다.

#### Many types of decompositions
- (Truncated) Singular Value Decomposition => Principal Component Analysis
- Non-negative Matrix Factorization
=> 아래 두 개는 Tensor 버전(다차원 버전)으로 더 확장을 한 개념
- Canonical Polyadic Decomposition
- Tucher Decomposition

#### Related work
Channel pruning
-> Structured pruining

채널 단위로 pruining을 하게 되면 Tensor 하나에서 어떤 규격화된 모양을 뜯어내는 것이 되기 때문에 연관된 work라고 볼 수 있다.

#### Network decoupling
Regular convolution과 depthwise separable convolutions의 수학적 관계를 증명

#### MobileNet
MobileNet은 CP Convolution의 special case에 불과하다는 내용을 수식적으로 증명

## Retrospect
Bootstrapping
****
