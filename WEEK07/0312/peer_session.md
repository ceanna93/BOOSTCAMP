데이콘 관련 질문

모델 저장 및 호출

https://tutorials.pytorch.kr/beginner/saving_loading_models.html

실제로 저장이 잘 되지는 않음. 원인 파악 

model.state_dict()로 저장하는 방밥과 pch로 저장하는 방법이 있는데 state_dict로 저장할 경우 모델이 선언되어 있어야하고, pch로 저장할 경우 모델은 없어도 되지만 모델 자체를 저장하는 것이기 때문에 내부에 선언되었던 경로가 이전과 완전히 일치해야 한다.
