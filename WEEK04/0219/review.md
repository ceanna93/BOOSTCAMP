Greedy라는 한계점

## GTP-1 
비영리 기관

자연어 생성에서 놀라운 결과

특징: 다양한 special tokens를 제안해서 심플한 task 뿐만 아니라 다양한 자연어 처리에서의 많은 task를 동시에 처리할 수 있는 통합된 모델을 제안

## BERT
현재까지 가장 널리 쓰이는 pre trained model

GPT1의 경우 standard한 language model로 전후 단어를 고려하지 않는다는 문제.

앞 뒤 문맥을 보고 단어 유추가 가능해진다. 따라서 왼쪽, 오른쪽을 보고 유추

## Masked Language Model
MASK를 하고 각 단어가 무엇인지 맞추는 형태로 학습이 진행

몇 % 단어를 mask로 치환해서 맞추도록 할 지 사전에 잘 결정해줘야 한다.

hypter parameter

pre trained 당시에 주어진 양상이나 패턴이 main task에서 주어진 입력과는 다른 특성을 보일 수 있다. 상이한 차이점이 학습을 방해하거나 transfer learning의 효과를 올리는데 문제가 될 수 있다.
mask로 치환하는 15% 단어들을 서로 다른 형태로 변환
80%는 [MASK]로 치환
10%는 random work로 변경
10%는 동일한 단어로 유지

## GPT-2
transformer 모델에 layer을 더 쌓아 모델을 키우고, Pre training task는 Language Modeling task. 다음 단어 예측

## GPT-3
더 많은 파라미터를 가지고 tranformer self attention block을 쌓은 모델, 데이터, 큰 배치 사이즈


Zero-shot setting에서 번역에 대한 데이터 

One-shot이 성능이 훨씬 좋다

Few-shot은 더 유의미하게 높은 성능

별도의 fine tuning 과정 없이 GPT-3 모델을 그대로 가져와 예시를 보여주고 하나의 sequence 내에서 pattern을 빠르게 학습하고 task를 수행

큰 모델을 사용할수록 동적인 적응 능력이 뛰어나다.

## LBERT (Lite BERT)
Pretraining 모델들은 대규모의 메모리 요구량과 학습에 필요로 하는 많은 모델 parameter를 가지는 형태로 발전

기존의 BERT 모델의 Obstacles를 해결하기 위한 모델

### Factorized Embeddign Parameterization
Residual connectoin


입력에 주어지는 word embedding의 embedding vector의 dimension 수

Skip connection이 존재하여 동일한 dimension이 유지

dimension이 작으면 정보를 담을 수 있는 공간이 적어지게 되는 단점

dimension이 크면 모델 사이즈도 커지고 연산량도 증가하는 단점

self attention block또는 layer를 쌓아나가면서 점점 더 high level의 (semantically)의미론적으로 유의미한 정보들을 계속적으로 추출하는 과정이 딥러닝에서 layer를 쌓는 과정으로 볼 수 있는데 첫번째 layer에서 word 별로 주어지는 word가 문장 내에서 갖는 관계, contextual한 관계를 고려하지 않고 각 word 별로 독립적으로 상수 형태 vector로 주어지는 embedding layer가 있을 때 embedding layer에서 가지는 word의 정보는 위에서 전체 sequence 혹은 그 문장을 고려해서 각 단어들을 encoding 해서 정보들을 저장해야 하는 hidden state vector들에 비해서는 적은 정보만을 저장하는 정도로도 충분할 수 있게 된다.

lbert에서는 embedding layer의 dimension을 줄이는 기법을 제시


고정해서 사용해야 하는 dimention이 4개라고 생각하면 일반적으로 word가 가지는 embedding vector에 position encoding을 더해준 형태로 진행

embedding layer에서는 각각의 word들이 self attention block에서 사용되는 dimension과 동일한 dimension을 어쩔 수 없이 가져야 하기 때문에 word embedding dimension도 4차원 vector가 주어져야 한다.

이 경우 word embedding 입력을 주기 전에 vector의 차원을 줄여 필요로 하는 파라미터와 계산량을 줄일 수 있는, 첫번째 레이어에서 계산량이나 모델 사이즈를 줄어들 수 있도록 하는 형태

추가적인 layer 하나를 더 둬서 dimension을 low rank matrix factorization 기법을 통해 전체적인 parameter 수를 줄여준다.



pre-training model이란?

## ELECTRA
- Generator: BERT모델로 생각
- Discriminator 존재가 가장 큰 특징
- Discriminator 모델은 Transformer에서 제안된 Self attention을 쌓은 모델
- 각 단어별로 예측을 하는데 이진분류로써 원래 있던 단어인지, 예측에 의해 채워진 단어인지 예측하는 모델
- 두 모델이 적대적 관계
- Generative adversarial network(GAN)
- Language Modeling, 자연어 처리에서의 Pre-training 모델을 제안
- Discriminator를 Fine-tuning된 Pre-train된 모델로 사용

경량화 모델의 연구 추세는 모델의 크기를 줄이고 계산 속도를 빠르게 하는데 클라우드나 고성능의 리소스를 사용하지 않고도 휴대폰에서 적은 양의 전력 소모 배터리 소모량으로 빠르게 계산을 수행하고자 할 때 주로 사용

모델을 계산하는 방법
- DistillBERT
- TinyBERT


## (실습) BERT 불러오기
BertTokenizer와 BertModel은 반드시 같은 bet_name을 불러와야 한다.
왜냐하면 Tokenizer와 Model은 함께 대량 데이터로 학습이 됐는데, 만약 Tokenizer에서 구축한 vocab 수나 token의 단위 실제 모델이 가지고 있는 embedding space와 일치하지 않게 되면 단어를 엉뚱한 인덱스로 인식하든지 엉뚱한 임베딩을 만들게 되는 문제가 생길 수 있다.
