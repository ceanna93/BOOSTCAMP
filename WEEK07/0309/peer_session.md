LSTM
input tensor(sample id, time, 1, feature)
output tensor = (sample id, time은 다르다, feature)
메모리 용량이 엄청날 텐데...

output feature의 시가 예측이 목표

배치사이즈=sampleid

각각의 데이터는 sampleid는 평행세계 (코인 거래소가 각기 다른 것과 유사)
각각의 sampleid에서 얻은 수익 합산

Transformer를 적용할 수 있을까
Seq2Seq 적용이 가능할까
