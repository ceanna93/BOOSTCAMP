## SOM-DST
SOM-DST의 [WarmupLinearSchedule](https://huggingface.co/transformers/v1.2.0/_modules/pytorch_transformers/optimization.html)
- 선형 워밍업 후 선형 감쇠
- 'warmup_steps' 학습 단계에 거쳐 학습률을 0에서 1로 선형적으로 증가
- 남은 t_total - warmup_steps의 단계 동안 학습률을 1에서 0으로 선형적으로 감소

위 Scheuler를 사용하는 이유?
