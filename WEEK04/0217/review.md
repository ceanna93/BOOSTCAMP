# sequence to sequence(Seq2Seq)
Sequence를 Encoding와 Decoding

Sequence to sequence는 encoder와 decoder로 이루어져 있는 framework으로 대표적인 자연어 처리 architecture 중 하나

RNN과 Attention을 결합한 sequence to sequence 모델
RNN 모델이 갖고 있는 단점을 보완하고자 Attention(논문에서는 alignment로 표현되고 있습니다) 기법이 처음 등장

Sequence-to-sequence
many to many 구조
출력 sequence를 생성 또는 예측하는 모델
word 단위의 문장

ENCODER 이후의 hidden state vector는 DECODER RNN의 h0로, 첫번째 time step의 입력으로 주어진다.

Seq2Seq Model
RNN 기반의 모델 구조가 Sequence의 앞에서부터 정보들을 읽어들이고 time step마다 hidden state vector를 생성.
hidden state vector는 RNN의 구조 특성상 항상 dimension이 정해져있다.

RNN과 LSTM의 문제
- 마지막 time step의 hidden state vector에 많은 정보를 넣어야 하는 문제
- dimension이 3차원 vector로 되어 있을 때도 고정된 hidden state vector에 sequence 전체 정보를 압축하여 저장해야 한다.
- LSTM에서 long term dependencies 문제를 해결했더라도 점차로 정보가 변질되거나 소실될 수 있다.
- 앞쪽에 나타난 정보를 잘 저장하지 못하는 현상이 나타나게 된다.

Attention을 사용하게 되면 Encoder의 마지막 time step에서 나온 hidden state vector에만 의존하는 것이 아니라, 입력 문장에서 주어진 각각의 단어들을 순차적으로 encoding 하는 과정에서 나온 encoder hidden state vector들을 전체적으로 decoder에 제공. Decoder에서는 각 time step에서 필요한 encoder의 hidden state vector를 선별적으로 예측에 사용

## Seq2Se2 with attention

Attention 모델의 ouptut이라고 볼 수 있는 encoder hidden state vector의 가중평균된 vector를 context vector라 부른다.
Softmax layer의 output인 가중치 vector(context vector)는 attention vector라고도 불리며 합이 1이 된다.
Attention 모듈은 decoder hidden state vector 하나와 encoder hidden state vector 전체가 attention 모델의 입력이 된다.
출력은 context vector

END 토큰이 나올 때까지 반복
학습 때는 예측되는 값이 다음 time step의 입력으로 사용되지 않고 ground truth를 입력으로 주게 된다.
=> Teacher Forcing 방식
학습이 빠르고 용이하지만 테스트 상황과는 다르다.

Teacher Forcing이 아닌 방식(ground truth를 입력으로 주는 것이 아닌, 이전 출력을 입력으로 넣는 방법)이 실제 모델 사용 상황과 가깝다.

Teacher Forcing 방법과 Teacher Forcing이 아닌 방법을 적절히 결합한 방식
초반엔 Teacher Forcing만으로 진행하다가 학습의 후반부에는 Teacher Forcing이 아닌 방식으로 학습을 변화시키는 방식

score($h_t$, $\bar{h}_s$)
$h_t$: decore의 hidden state vector
$\bar{h}_s$: encoder 단에서의 각 단어 별로 hidden state vector

### 내적
### generalized
서로 다른 dimension 간의 곱셈 값들에 각각 부여되는 가중치 = 행렬

### concat
Decore의 hidden state vector, encoder의 hidden state vector를 내적하는 방식을 달리 하여, 두 vector 간의 유사도를 구하는 Scalar 값을 구하는 방법

multi layer neural net 또는 multi layer perceptron이라고 불리는 학습 가능한 neural net을 만들 수 있다.



### Greedy decoding
Sequence로써의 전체적인 문장의 확률 값을 보는 것이 아니라 현재 time step에서 가장 좋아보이는 단어를 선택하는 형태
Greedy approach 

현재 확률값이 조금 작아지더라도 뒤에서 상대적으로 더 큰 확률값을 가지게 될 수 있는 선택을 앞에서 하는 것.
전체적인 joint probability의 값을 최대화 하는 게 더 좋은 결과를 낼 수 있다.
경우의 수가 너무 많아지기 때문에 차선책으로 나온 방법이 **Beam search**

Greedy decoding과 가능한 모든 경우를 따지는 방법 중간의 접근 방법
Decoder의 time step마다 K개의 가능한 가지수를 고려하고 time step이 진행함에도 K개의 경우의 수를 유지하고 마지막까지 decoding을 진행하고 최종적으로 나온 확률들 중 가장 확률이 높은 것을 택하는 방식

최대화하는 부분은 joint probability
$P_\mathit{LM}(y_1, ..., y_t|x)$
log를 붙이게 되면 덧셈으로 식이 변경
$\displaystyle \sum_{i = 1}^t{logP_\mathit{LM}(y_i|y_1, ..., y_\mathit{i-1}, x)}$
단조증가 함수기 때문에 확률이 가장 큰 경우 로그를 취한 값도 가장 큰 경우로 유지

길이로 평균을 취하면 아래 식이 된다.
$score(y_1, ..., y_t) = \frac{1}{t}\displaystyle \sum_{i = 1}^t{logP_\mathit{LM}(y_i|y_1, ..., y_\mathit{i-1}, x)}$

Greedy decoding의 경우 생성을 끝내는 시점은 END token을 time step에서 예측 단어로 예측했을 때
Beam search decoding의 경우 각각 다른 시점에서 END token을 생성할 수 있기 때문에 END token이 생성되면 저장 공간에 임시로 저장하고 남은 예측들에 대해 END token이 발생할 때까지 예측을 계속한다.

질문. K가 3이고 1개의 예측이 END된 경우 2개의 예측에 대해서만 진행을 하려나. 만약 임시로 저장한 값들보다 큰 확률 값이 3개 나타난 경우.

time step의 최댓값을 설정하고 time step이 해당 설정에 도달하거나 완료된 예측의 개수(End token을 만난 횟수)가 설정된 개수가 되면 beam search 종료

문제: hypotheses의 길이가 서로 다를 경우 짧은 길이의 hypotheses가 joint probability 값이 더 높다.
항상 음수 값을 더해주기 때문에 길이가 길어질수록 joint probability 값이 더 작은 값으로 나오게 된다.
공평하게 비교하기 위해서 각 hypothesis 별로 단어의 개수로 나누어 준다. 단어 당 평균 값.

BLEU score
정밀도 : 예측된 결과가 노출되었을 때 사용자가 실질적으로 느끼는 정확도
검색 시스템에서 특정한 키워드로 검색을 했을 때 검색 결과 문서들이 원하는 정보, 의도에 부합하는 문서들이 나온 경우 검색 결과가 만족스럽다고 생각. 눈으로 보고 판단할 수 있는 대상.
재현율 : 검색 시스템에서 키워드를 가지고 검색했을 때 키워드에 관련된 문서들 중 실제로는 검색 키워드에 부합하지만 결과에 노출되지 않은 문서들에 실제로 필요로 하는 정보들이 존재할 수 있다. 의도에 부합하는 문서의 개수 중 몇 개를 사용자에게 노출시켜주었는지.

순서도 성능 평가에 포함하기 위해 BLEU score 이용
precision만을 고려
brevity penalty를 사용
길이만을 고려했을 때 groun truth보다 짧아졌을 때 짧아진 비율만큼 precision 값을 낮춰준다. recall의 최댓값을 의미.
brevity penalty에서 recall을 고려
