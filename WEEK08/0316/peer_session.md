## 1. DACON 
###  1) 진행상황 공유
window size를 통해 예측하는 방법과 트랜스포머를 사용하는 방법, 크게 두 가지로 콘테스트를 진행하고 있습니다. 다만 현재 전처리와 모델 학습에서 어려움을 겪고 있는 분들이 많아 지금은 한 가지 feature만을 사용하는 방법으로만 결과를 예측하고 있고 이에 많은 한계를 느끼고 있습니다.
###  2) 나왔던 질문내용 
- 각 sample_id마다 새로운 모델을 만들어 사용하는지?
- window size를 100으로 잡았을 때 데이터를 새로 만들기 위해 append를 사용하니 너무 오래걸리는데 더 좋은 방법이 있는지?
- transformer에서 pre-trained model로 사용하고 cell time과 buy quantity를 output으로 내는 방법(end-to-end)에 대한 토론
- numpy와 list의 크기 차이. 실제 메모리에 할당되는 시간은 numpy가 list에 비해 오래 걸린다. 접근하는 데 걸리는 시간은 비교해보지 못 했음
## 2. 멀티쓰레드 / 멀티프로세스 파생 궁금증 질문
- multiporcessing.Manager? 
일반적인 전역변수는 멀티프로세싱에선 서로 자원을 공유하지 않습니다. 프로세스 간 객체를 공유하는 데 사용할 수 있게 제작된 SyncManager 객체를 사용할 수 있게 해주는 모듈로 dict, queue, list 등을 사용할 수 있습니다.

---종혁님 피어세션 정리


multiprocessing에서 manager을 이용하여 자원을 공유할 경우, 시간이 오래 걸릴 수 있다

http://stackoverflow.com/questions/17421220/shared-list-multiprocessing-manager-list-is-very-time-consuming
