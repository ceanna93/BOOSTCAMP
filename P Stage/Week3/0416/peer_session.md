#### validation
training dataset으로 validation으로 하는 것은 의미가 없을 수 있다. 정확도 결과가 비슷하게 나오고 overfitting 없고 분포가 다르기 때문에.

#### KoBERT나 KoELECTRA, RoBERT 변경 시 점수 상승이 되지 않을까
#### maxlength를 변경하면 정확도가 오른다.

#### 지금 데이터셋에서 KoELECTRA가 UNK이 더 적게 나온다.

### UNK이 발생했을 때 성능이 좋지 않은 이유 추측
UNK 처리된 토큰은 모두 동일한 UNK으로 처리될 수 있다고 생각한다.

UNK을 vocab에 넣어도 성능이 좋지 않다.

corpus에 실제로 들어있지 않기 때문에 문맥을 이해하기 쉽지 않다.

새로 vocab을 넣어주면 랜덤 가중치가 생성되고 학습을 다시 해줘야 의미가 있지 않을까.

새로운 vocab의 가중치를 계산해줘야 한다.

#### special token에 대해서 어떻게 처리를 하는지??

tokenizing 이후 embedding

BertIntermediate

#### batch 크기가 nlp에서 중요한데 어느 정도가 적절한 크기인지. epoch 당 step이 중요하지 않나.

#### automodel이 좋다.
