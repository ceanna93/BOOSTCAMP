seed는 최적화의 대상은 아니지만 seed에 따라 순위가 달라지기도 한다.

batch size가 커질수록 sharp minima에 걸릴 확률이 높다. 동일한 epoch에서 batch size를 키우면 학습 횟수가 적어 업데이트 횟수가 적어진다.
batch size와 learning rate는 어느 정도 연관이 있다.

Augmentation을 했을 때 성능이 오히려 떨어진다. => 원인 파악
