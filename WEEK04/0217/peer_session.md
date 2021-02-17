# 02/17 Peer Session

## Q&A
1. Seq2Se2
    RNN의 단점 보완
    LSTM, GRU가 Long term dependencies 문제를 완벽하게 해결한 것은 아니다.
    
    사람의 인지를 생각했을 때 Seq2Seq보다 LSTM의 forget gate가 사람의 인지 과정과 비슷하지 않을까.
    수능의 비문학 지문을 읽을 때 뒤의 지문을 읽으면서 앞의 지문을 잊는 것과 비슷하게
    => 사람의 뇌보다 더 좋은 기능을 하는 것이 인공지능의 목적이 아닐까 생각했음
  
2. Seq2Seq with attention에서 Cost function의 계산
Teacher Forcing의 경우 라벨이 존재한다고 생각할 수 있다. 하지만 라벨이 없는 상태에서 초기 학습은 어떻게 올바른 값인지 판단하는지.
초기값을 설정해줄지.
처음부터 Teacher Forcing을 하지 않으면 라벨이 존재하지 않는 상태로 학습을 하게 되는 것이 아닌지.
    
    학습을 진행할 때 초기엔 Teacher Forcing, 이후 입력은 이전 스텝의 출력을 입력으로 사용.
    Cost Function이 어떻게 계산되는지에 대해선 논의되지 않음
    
3. Seq2Seq의 Attention과 Self Attention의 차이
    Seq2Seq with attention에서는 RNN을 사용
    단어 별로 한 번에 계산
    
4. 단어가 수십만이 있을 때 그 중 하나를 고르는 방법. 전체 단어에 대해 Softmax와 One hot encoding을 하는지. 
단어가 무수히 많이 존재한다면 Softmax와 one hot encoding을 하는 작업에서 수많은 0을 처리해야 하기 때문에 자원 낭비가 발생하지는 않을지.
Sparse한 Matrix
embedding을 통해 해결할 수 있는지
    https://simpling.tistory.com/1
    
5. one hot encoding에서 차원을 줄여도 정보 손실은 일어날 확률이 적지 않을까
    캐글에서 차원이 큰 비정형 데이털르 embedding하여 학습한 결과 loss가 줄지 않고 정보 손실이 컸음.
    정확도가 낮은 문제.
    
    다중 분류에선 one hot encoding을 사용해줘야 한다.
    
    one hot encoding을 사용하지 않으면 embedding의 경우 정보의 손실이 클 수 있다. Cost를 믿을 수 있는지 의문.
    one hot encoding은 자원 낭비가 존재하지만 정보 손실은 발생하지 않을 것이다.
    
6. Beam search에서 END 토큰이 나왔을 때 왜 Bucket에 담아두는지. 매번 END 토큰을 만날 때마다 최댓값을 비교하여 갱신해주면 안 되는 이유
    

  
+ 개인적인 궁금증
  - Softmax에서 동일한 확률이 발생하는 경우는 없을지. 동일한 경우가 발생한다면 one hot encoding을 어떻게 동작하게 되는지.
  - [차원의 저주](https://datapedia.tistory.com/15)
