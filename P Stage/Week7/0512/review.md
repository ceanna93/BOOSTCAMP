## SOM-DST
### SOM-DST의 코드에서 의문.
- model_evaluation 함수를 보면 make_turn_label에서 i.gold_state를 사용한다. gold_state는 현재 turn의 state 값이므로 모델의 inference를 이용해 state를 추출한 값을 사용하는 것이 아니고, ground truth를 사용하는 것이라고 생각된다. state가 없는 대화에서 state를 추출하기 위해 방법을 수정해야 한다고 생각했다.
