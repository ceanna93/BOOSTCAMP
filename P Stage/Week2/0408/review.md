## 결과
1. Validation X + K Fold 방식은 Overfitting이 발생한 것처럼 정확도가 매우 낮았다.
2. Model을 분리한 후 epoch 증가하여 각 모델의 정확도를 높였을 때의 결과가 가장 좋게 나왔다.

WeightedRandomSampler는 데이터를 꺼낼 때 가중치에 따라 꺼내오는 양이 달라지는 sampler라고 알고 있는데 왜 Imbalance 데이터에 사용하는지 알 수 없음.
