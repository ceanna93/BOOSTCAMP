load_dataset 함수에서 1개가 더 train 쪽으로 가는 원인(아래처럼 train은 6301, dev는 699개가 되는 이유)
6301/699

3개의 도메인에서 233개씩 가져온다.

- domain 2 : 3100
- domain 1 : 1661
- domain 3 : 2239

stratified k fold나, 다른 validation 방법 필요. 각 도메인 별 비율로 검증이 필요

+ dialogue에서 이용자가 중간이나 마지막에 마음을 바꾸는 경우가 존재하는지 확인 필요

tokenizer = BertTokenizer.from_pretrained('kykim/bert-kor-base')

tokenizer에 사용되는 pretrained된 방법을 바꿔줘도 성능 향상에 효과가 있다.

train에 없는 데이터는 SUMBT에서 처리해주지 못 한다.
=> SUMBT를 사용할 거라면 부족한 데이터를 채워넣을 필요.


**Unseen Slot Value**와 **CounterFactuals**
=> 두가지에 대한 고려 필요

Open-Vocab based DST model
=> 없는 데이터도 유추가 가능한지 확인
