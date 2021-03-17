## 빠르게
### 미니코드
python list와 numpy의 실행 속도가 다른 이유

### 가속 (Acceleration)
C++

network의 bottleneck 해결

CPU - Parallel processing
Througput

Machine Learning에서 bottleneck은 model의 layer가 쌓여있는 구간

Hardware acceleration

general-purpose보다 좀 더 빠르게 진행하고 싶을 때 hardware acceleration.

### Compression: Acceleration
Compression과 Acceleration은 Tightly coupled
- Compression: Software(high level쪽에서 주로 사용)
- Acceleration: Hardware(low level쪽에서 주로 사용)

### Deep learning compiler
high level단의 프로그램을 해석할 수 있는 언어로 변경

High Level Language -> (Compiler) -> Assembly Language -> (Assembler) -> Machine Language

The Deep Learning Compiler: A Comprehensive Survey.

Model을 input으로 받는다. generate optimized codes for diverse DL hardware as output.

MLIR(Multi-Level Intermediate Representation)

### Locality of reference
- Temporal locality
- Spatial locality
- Branch locality
- Equidistant locality

## 가지치기(Pruning for network compression)
### 미니코드

**Weighted sum model**
-> Pruning에서 중요한 작업

Pruning
- 장점
	- Inference speed
	- Regularization (lessen model complexity) brings generalization
- 단점
	- Information loss
	- The granularity affects the efficiency of hardware acclerator design

Dropout은 잘라낸 weight를 inference할 때 전부 복원한다. Training epoch에 따라 켜지는 weight도 달라진다.

Structured Pruning
	- neuran을 잘라낸다.
Unstructured Pruning
	- weight를 잘라낸다.

Iterative pruning
한 번에 weight를 줄여버리면 retrain을 해도 accuracy가 향상이 일어나지 않는다.

### Lottery Ticket Hypothesis
논문의 한계
- 증명되지 않았다. 
- original training을 해야만 lottery를 알아낼 수 있다.
의의
- 존재성은 밝혀냈다.
- 높은 확률로 lottery ticket이 존재한다.

어떻게 하면 lottery ticket을 찾아낼 수 있을까.
1. Iterative magnitude pruning with Rewinding
