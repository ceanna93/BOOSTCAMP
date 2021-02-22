# WEEK 04 Further Questions

## Word2Vec과 GloVe 알고리즘이 가지고 있는 단점은 무엇일까요?
word2vec에서 입력이 수많을 때 단어 하나마다 vector값을 만들어 학습시키는지.
중복되지 않는 word의 개수가 10만개라면 하나만 1이고, 나머지 위치들(9만 9999)개는 0으로 된다.

동음이의어에 대해 word2vec의 성능
벡터의 의미가 퇴색이 되지 않을까. 동음이의어를 둘 다 학습하게 된다면
두 단어가 모두 다른 의미를 가진 단어들과 연관성이 높아야 한다.
배가 ship, pear가 있을 때 선장과 먹었다와 의미가 유사해야 하는데 그 두 상황을 고려해 중간 합의점을 찾는다. embedding된 값을 찾는다. 단어를 제시했을 때 유사도가 높은 단어를 찾아준다. 배는 어떤 단어들과 연관성이 높은지, 거리로도 가능

한국어에선 잘 안 된다.
영어도 Attention이 나온 이후부터는 사용되지 않는다.

Word2Vec 신경망이 현재는 사장됐다? Input 값으로서 임베딩 되는 의미는 많이 사장됐지 않았나.
유사한 정도를 볼 때는 많이 사용된다. 시각화에선 필요.
결과를 빠르게 시각화를 하고 싶을 때 장점
현업에서는 도움이 될까? 개념적인 공부를 위해서만 도움이 되는 신경망이 아닌가.

Word2Vec, GloVe 이후 나온 기법
ELMo
https://wikidocs.net/33930
비슷한 임베딩 방법
동음이의어에 대해 벡터 값이 다르게 나와 LSTM을 이용.

## BPTT 이외에 RNN/LSTM/GRU의 구조를 유지하면서 gradient vanishing/exploding 문제를 완화할 수 있는 방법이 있을까요?
## RNN/LSTM/GRU 기반의 Language Model에서 초반 time step의 정보를 전달하기 어려운 점을 완화할 수 있는 방법이 있을까요?
Back Propagation Through Time

BPTT 이외에 RNN/LSTM/GRU의 구조를 유지하면서 gadient vanishing 완화
=> 양방향 학습 (완화까지는)
=> Seq2Seq, Transformer의 방법

2.2 핍홀(peephole) 연결
핍홀 연결(peephole connection)은 2000년에 F. Gers와 J.Schmidhuber가 'Recurrent Nets that and Count' 논문에서 제안한 LSTM의 변종이다. 기존의 LSTM에서 gate controller(​)는 입력 ​와 이전 타임스텝의 단기 상태 ​만 입력으로 받는다. 하지만 위의 논문에서 제안한 핍홀 연결을 아래의 그림과 같이 연결 해주면서 gate controller에 이전 타임스텝의 장기 상태 ​가 입력으로 추가되며, 좀 더 많은 맥락(context)를 인식할 수 있다.
https://excelsior-cjh.tistory.com/185 [EXCELSIOR]

단기상태만 업데이트하던 OutputGate에 장기상태까지 추가해서 업데이트

## BLEU score가 번역 문장 평가에 있어서 갖는 단점은 무엇이 있을까요?
- It doesn't consider meaning.
- It doesn't directly consider sentence structure.
- It doesn't handle morphologically rich languages well.
- It doesn't map well to human judgements.
- One problem with BLEU scores is that they tend to favor short translations, which can produce very high precision scores, even using modified precision.

## Attention은 이름 그대로 어떤 단어의 정보를 얼마나 가져올 지 알려주는 직관적인 방법처럼 보입니다. Attention을 모델의 Output을 설명하는 데에 활용할 수 있을까요?
참고: Attention is not explanation
참고: Attention is not not explanation
각각의 단어에서 어떤 단어들이 유사한지 활용할 수 있다?

가중치를 가지고 어떤 단어를 설명할 수 있는가.
가중치로 변수를 설명하기 불가능하다.
random forest, light gbm은 인간의 한계를 뛰어넘어 블랙박스 모델
V1부터 V10의 계수를 구할 수 없다.
black box 모델이 왜 생기는가.
decoder로 나오는 모델이 왜 그렇게 나오는지 알 수 없다.
서로 가중치들의 값이 얽히기 때문에 마지막 출력 단에선 어떤 단어가 가장 큰 값을 나오게 만들었는지, 영향을 끼쳤는지 계산하기 어렵다. 설명이 불가능하다.
레이어가 깊어질수록 비선형, 어떤 변수가 중요한지 설명할 수 없다.

어텐션만이 아니라 모든 딥러닝을 통하는 문제

## BERT의 Masked Language Model의 단점은 무엇이 있을까요? 사람이 실제로 언어를 배우는 방식과의 차이를 생각해보며 떠올려봅시다

### BERT의 Masked Language Model에서 Masked되는 위치는 Random?
Random이어서 연달아 나타날 수 있다. 하지만 대량의 데이터를 학습시키면 연이어 나타나도 문제 없이 학습할 수 있다.

pre-training 과정에서는 주어진 문장에서 평균적으로 15% 단어가 masking된 단어로 이루어져있는 문장에 익숙한 모델이 학습되는데, 이 모델을 main task에 수행할 때는 mask라는 토큰은 더이상 등장하지 않게 된다.
train에서 나오는 양상이나 패턴이 main task를 수행할 때 주어지는 입력에 대한 문장과는 다른 특성을 보여 학습을 방해하거나, 성능을 올리는데 방해요소가 될 수 있다.

실제 데이터는 마스크 되지 않은 fine tuning에서는 마스크 되어 있지 않기 때문에 예측 결과를 방해할 수 있다.
나중에 모델을 Fine tuning 할 때는 MASK를 사용하지 않기 때문에 단점이 될 수 있다.
GPT는 앞의 내용만 가지고 뒤의 값을 예측하기 때문에 마스킹 된 것과 동일. 실제 main task에서는 pre-train된 상황과 다르게 수행

## BERT는 GPT2, GPT3보다 성능이 떨어지는지?
GPT3의 성능은 BERT보다 훨씬 좋다.

pre train을 하지 않아도 fine tuning을 하니까 성능이 나온다.
어떻게 가능한지
각자, 영어, 프랑스어로 학습을 시키고, 번역에 대한 학습을 하지 않은 상태에서 영어로 된 문장을 프랑스어로 번역하라고 시켰을 때 번역을 잘 하지 않았을까.



딥러닝이 왜 블랙박스인가.
머신러닝 또란 마찬가지.

소프트맥스 자체가 비선형
