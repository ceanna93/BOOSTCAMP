## Competition
SOM-DST의 encoder에서 전부 carryover만 예측하는 문제를 해결하기 위해 아래 방법으로 CrossEntroyLoss에 weight 추가
```
count_label = [0] * int(args.op_code)
for ins in train_data:
    for op_id in ins.op_ids:
        count_label[op_id] += 1

weights = [1 - (x / sum(count_label)) for x in count_label]
print(weights)
class_weights = torch.FloatTensor(weights).to(device)
loss_fnc = nn.CrossEntropyLoss()
loss_weight_fnc = nn.CrossEntropyLoss(weight=class_weights)
```
loss_fnc은 도메인의 손실을 확인하기 위해 weight를 주지 않고, state_scores의 손실을 계산하는 함수에만 weight을 추가하였다.

```
[0.9999567917335209, 0.9716938430854918, 0.994595805109641, 0.03655366651122227, 0.9973864268080948, 0.9998134667520293]
```
op_code를 6으로 주었을 때 위와 같은 weight을 가지게 된다. 수정하면서 mean_loss가 weight을 사용하지 않았을 때보다 약간 느리게 감소한다.
