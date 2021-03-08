Self-training에서 Teacher-student 과정 중 augmentation이 없어도 성능 향상이 나타날까?
처음 Student가 Teacher이 됐을 때, 학습, accuracy가 높아지는 과정은 이해할 수 없다. 동일한 bias가 생기기 때문에.
결국 하나의 값으로 수렴하지 않을까.
큰 성능 차이가 발생하지 않기 때문에 2~3번만 하지 않을까

Knowledge distillation에서 가중합(Weighted sum)은 사용자가 설정하는 것인가 (학습 파라미터인지, 하이퍼 파라미터인지)?

https://keras.io/examples/vision/knowledge_distillation/
알파 베타로 표시하기 때문에 하이퍼 파라미터로 생각됨.

