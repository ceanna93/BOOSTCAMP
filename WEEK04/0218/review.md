# Transformer
Attention is all you need: add on 모듈이 아닌 RNN 또는 CNN을 대체한다

RNN은 정보를 축적하여 히든 스테이트 업데이트

RNN에서 히든 스테이트를 거치는 과정에서 발생하는 손실, 유실

## Bi-directional RNN
Forward RNN hidden state vector와 Backward RNN의 hidden state vector를 concat하여 전체적인 정보를 고려하여 encoding vector를 만드는 방법

## Transformer: Long-Term Dependency
Attention이 적용되는 방식은 Seq2Seq with attention에 적용되는 방식과 유사


자기 자신과 내적이 될 경우 서로 다른 vector와 내적을 했을 때보다 훨씬 큰 값으로 도출. 자기 자신에 큰 가중치가 걸리는 형태로 attention vector 양상이 나타남

자기 자신의 원래 정보만을 주로 포함한 vector들만 출력된다.

가장 기본적인 형태의 Attention의 문제점을 개선한 형태의 모델

주어진 입력 vector에서의 각 단어에 해당하는 encoding vector를 얻어내기 위해서는 input vector가 decoder hidden state vector인 것처럼 하여 주어진 벡터들의 가중치, 유사도를 구하는 vector로써 사용. 주어진 vector들 중 어느 vector를 선별적으로 가져올 지 기준이 되는 vector로써의 역할하는데 이를 query라고 표현

주어진 encoder hidden state vector의 각 vector와 내적을 통해 유사도가 구해지는데, 유사도가 계산되는 query vector와 내적이 되는 각각 재료 vector들을 key vector라고 표현

어떤 key vector가 높은 유사도를 갖고 있는 지.

query vector를 통해 주어진 여러개의 key vector들 중에 어느 key vector가 높은 유사도를 갖고 있는지. 유사도 및 어느 것을 갖고 올 지 결정해주는 역할이 key vector.

각각의 키와의 유사도를 구한 후 softmax를 취한 후 가중치를 적용하여 가중평균, 선형 결합을 했을 때 사용하는 재료 vector(단어 벡터)들은 key vector와 동일한 vector로 취급해서 key vector를 구하는데 사용했지만 또 key를 구하기 위한 재료 vector들로 사용되면서 Values vector라고 부르게 됨

각 vector들이 Queries, Keys, Values 역할을 모두 하게 된다.

Transformer에서 제안된 Self attention 모듈은 동일한 Set의 vector에서 출발해도 각 역할에 따라 벡터가 서로 다른 형태로 변환할 수 있도록 해주는 별도의 linear transformation matrix 혹은 주어진 vector가 각각 query, key, value로 변환될 때 적용되는 선형변환 가중치가 따로 정의되어 있다.

주어진 같은 vector에서 query, key, value로 사용될 때 각기 다른 vector로 변환될 수 있는 확장된 형태가 만들어지게 됨

각 hidden state는 value vector로 인해 모든 단어로부터 정보를 고려하여 결합한 결과 vector가 만들어진다.

sequence 길이가 길어도 self attention 모듈을 적용해 sequence 내 각각의 word들을 encoding vector들로 만들면 time step의 거리가 멀어도 동일한 key, value vector로 변환이 되고 query vector에 의한 내적에 의한 유사도만 높다면 time step의 거리가 멀리 있더라도 정보를 쉽게 가져올 수 있다.

=> RNN의 한계(Long term dependency) 개선한 형태

내적을 위해 query와 key의 vector 크기는 동일해야 한다.

## Scaled Dot-Product Attention

A(Q, K, V) = softmax(QK^T)V

실제 Transformer 구현 상으론 동일한 shape로 mapping된 Q, K, V가 사용되어 각 matrix의 shape는 모두 동일


softmax의 확률 분포가 분산이 큰 값에 몰리는 패턴이 나타날 수 있다.

분산이 작을 경우 확률분포가 고르게 나온다.

내적에 참여하는 query와 key vector의 차원이 몇이냐에 따라 내적값의 분산이 크게 좌지우지될 수 있고, softmax로부터 나오는 확률 분포가 어느 한 키에만 100%에 가까운 확률이 몰리는 극단적인 형태의 확률이 나오거나 전반적으로 모든 key가 고른 확률 값을 부여받은 확률이 나오는, softmax의 확률 분포의 패턴이 query와 key의 차원 때문에 영향을 받게 된다.

내적기반 유사도를 구할 때 
내적 값에 분산을 일정하게 유지시켜 학습을 안정화시키기 위해 내적값에 차원에 루트를 씌워 나눠주는 연산을 넣게 된다.


동일한 query, key, value vector에 대해 동시에 병렬적으로 여러 버전의 attention 실행

head_i = Attention(QW_i^Q, KW_i^k, VW_i^v)

### Multi-Head가 필요한 이유
동일한 sequence가 주어졌을 때도 특정한 query word에 대해 서로 다른 기준으로 여러 측면에서 정보를 뽑아와야 될 필요가 있을 수 있기 때문이다.

여러 문장으로 이루어져 있지만 주어진 하나의 sequence로 이루어져 있다고 생각할 수 있는 경우, 주체가 한 행동을 중심으로 하는 정보를 뽑아올 수 있게 되고, 주체가 존재하는 장소의 변화에 대한 정보를 추출할 수 있다. 병렬적으로 정보를 뽑고 정보들을 합치는 방식으로 어텐션 모듈을 구성할 수 있다.

각각의 head가 서로 다른 정보들을 상호보완적으로 추출하는 역할을 하게 된다.

Self Attention에서 주된 계산 부분을 차지하는 것은 Softmax(QK^T/sqrt(d))에서 QK^T 연산에서 가장 많은 시간을 차지

GPU가 크면 행렬 연산의 병렬화로 한 번에 계산이 가능하다.

Recurrent는 주로 필요로 하는 계산이 각 time step마다 h_t-1가 W_hh와 내적을 수행. time step 개수 n * 각 time step에서 일어나는 hidden state vector를 Whh에 의해서 변환할 때 계산량 d^2

forward propagation/backward propagation 과정에서 메모리에 모두 값을 저장해줘야 한다. 역전파에서 각 값들이 필요하기 때문에.

d는 hyper parameter로 사용자가 결정할 수 있다. n은 주어진 입력에 따라 가변적인 값이 됨.

따라서 sequence 길이의 제곱에 비례하는 Self attention은 RNN보다 더 많은 메모리가 필요로 하게 된다.

RNN은 각 time step에서 계산되는 hidden state vector는 절대 병렬화가 불가능

따라서 sequence 길이에 비례한 병렬화가 불가능한 Sequential Operations이 필요하다.

학습은 RNN보다 Self Attention보다 빠르게 진행이 가능하다.

### Maximum Path Length
Long-Term Dependency와 연관

길이가 n인 sequence에서 가장 끝에 있는 단어가 가장 앞에 있는 단어의 정보를 참조하기 위해선 n번의 RNN 레이어를 통과해야 한다.

Self attention은 거리에 관계없이 한 번에 정보를 가져올 수 있다.

## Block-Based Model

add + layer normalization을 수행

add -> (residual connection)을 적용하기 위해선 input과 encoding의 output dimension이 동일하게 유지되어야 각 dimension 별로 해당 원소 값을 더해 동일한 dimension의 vector를 만들 수 있다.

Fully connected layer: Feed Forward

## Layer Normalization

## Positional Encoding
순서를 바꿔도 각각의 단어는 key, value의 페어들은 순서에 상관없이 각 key 별로 주어진 query와의 attention 유사도를 구하고 해당 value vector에 가중치를 부여해 가중합을 함으로써 주어진 query vector에 대한 encoding vector를 얻어내는데 주어진 가중평균을 얻어낼 때 value vector들이 교환 법칙이 성립되기 때문에 최종 output vector는 순서에 관계없이 결과가 동일하게 된다.

순서를 무시하는 특성은 입력 문장을 sequence 정보를 고려해서 encoding을 하지 못하고 순서를 고려하지 않는 집합으로 보고 각 집합에서의 원소의 encoding을 얻는 과정으로 생각할 수 있다.

=> RNN과는 다른 차이점

RNN은 순서가 달라지면 정보가 쌓이는 순서가 달라지기 때문에 encoding vector들도 달라지게 된다.

Transformer, Self attention 모듈은 순서 정보를 반영할 수 없다는 한계점

=> Transformer: Positional Encoding이 나옴

각 순서를 특정지을 수 있는 상수 vector를 각 순서에 등장하는 word input vector에 더해주는 것.

더해주는 vector를 결정하는 방법은 sin, cos로 이루어진 주기 함수를 사용

서로 다른 주기를 사용하여 여러 sin 함수를 만든 후 발생된 특정 x 값에서의 함수 값을 모아서 위치를 나타내는 vector로 사용

위치 별로 서로 다른 vector가 더해지게 하여 위치 정보를 Transformer에 포함

## Warm-up Learning Rate Scheduler

## Decoder
### Multi-Head Attention
Decoder 단에서 만들어진 hidden state vector가 query로 사용되고 encoder 단의 최종 output이 key와 value로 입력되어 Attention이 수행

### Masked Multi-Head Attention
정보를 차단해줘야 한다. 대각선을 기준으로 윗부분은 모두 0으로 변환. 가중합이 1이 되는 방식으로 추가적인 후처리를 해준다.

Attention을 후처리로 보지 말아야 하는 뒤에서 나오는 부분의 가중치를 0으로 만들어주고 이후 value vector와 가중평균을 내는 방식으로 attention을 변형한 방식

