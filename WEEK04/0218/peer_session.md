# 02/18 Peer Session

## Q & A

- Transformer의 Encoder 부분에서 가중평균 벡터를 구하는 목적
    context vector를 구하기 위해
 
- Context vector를 구하면 Encoder Input vector와 동일한 차원인지.
    Key, Query는 동일하고, value는 다를 수 있지만 결국 동일하게 변경해준다. 크기를 맞춰준다.
    Dimension을 바꿀 순 있지만 shape를 맞춰준다.
    

- 실제 Transformer는 input을 따로 분리해 각각의 Head에 복사해서 넣어준다고 하는데 손실은 없는지

- Attention에서 Complexity per layer 계산식에서 d는 사용자가 정하는 파라미터인데, RNN에서 N을 왜 곱해줘야 하는지. 현재와 그 전 차원만 존재하면 값을 구할 수 있는 게 아닌가.
    RNN은 back propagation을 위해 N개를 보관하고 있어야 한다.
    
- Decoder라고 이름을 붙이려면 Encoder가 있어야 하는지
    있어야 한다.
    
- 언어 모델엔 batch normalization이 없는지
    언어에 Fully connected가 쓰이면 batch를 넣어줄 수 있지 않을까
