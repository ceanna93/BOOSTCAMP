## 모델의 시공간

답이라고 할 수 있는 것들의 집합을 Solution space(feasible region, feasible set, search space), 문제가 정의된 공간 자체를 Problem space

f(x) <= cg(x)
input 크기에 비해 얼마나 계산량이 폭증하는 알고리즘인가.

문제에 대하여 코드가 돌다가 끝나는 영역까지가 알고리즘
스텝이 무한번인 경우 알고리즘이라고 부르지 않는다.
알고리즘이 문제를 풀 때 비교적 소요하는 시간에 따라 클래스가 나뉘어진다.
Regular Langulages < Context-Free Languages < P < NP < Recursive Languages < Recursively Enumerable Langues

Machine Learning은 NP 문제에서 많이 사용
P이하의 문제들은 ML 수준의 문제 풀이는 필요 없다.

Multi Sort의 경우 Time-Space Trade-Off 문제

### Entropy
경우의 수

미래의 흐트러진 상태에서 과거의 정리된 상태로 된다.

엔트로피: inital state(low entropy, a particular state) -> high entropy(many possible states) -> Terminal state(low entropy, a particular state)

randome initalize는 high entropy 상태

### Optimization on search space
데이터, model도 다차원 공간 상의 한 점으로 표현이 가능하다.
=> 모델이 나타내는 공간 표현 가능

### Hypterparameer search
Hyperparameter: 사람이 골라주는 값
하이퍼파라미터마다 어던 결과가 출력될지 예측이 어렵다. 모델이 학습하는데 시간이 오래 걸린다.

search 한 번에 들어가는 cost가 굉장히 크다는 전제.

Parameter search와는 다른 연구 줄기가 나오게 됨

Search strategy
Set of candidate를 grid하게 만들고 전략을 고르는 것도 모델에 의해서 결정
Automatic neural architecture search

Architecture search 논문
- NaSNet-A
- DARTS
- MnasNet
- Proxyless
Candidate를 조합해 본 논문들

## 알뜰히
### 미니코드
Compression rate 계산

### Coding

Huffman coding
많이 등장하는 문자를 적은 비트로, 적게 등장하는 문자를 많은 비트로 압축하면 효율적

Finite State Machine(Machine)

Program

Set of language.

### Compression
압축률(크기, 성능)은 Pruning + Quantization이 가장 좋은 결과
