## 다른 팀원과의 피어세션
- 팀으로 구성되었다면 팀원을 온전히 믿고 latency가 발생하더라도 맡은 일을 끝까지 완수하는 것이 중요하다고 생각
- 안 풀리는 일을 주변에서 달려드면 오히려 능률이 떨어진다고 생각
- 논문 구현을 2\/2\/3으로 나눠서 수행
- 완성까지 결과와 의견은 공유하되, 참여하는 것보다는 팀원을 믿고 맡기는 게 필요

- 협업에 대해 고려했지만 각자 하고 필요할 때만 협업을 하는 방향으로 수정하면서 협업 효과가 좋았다.(개개인의 능력이 뛰어나기 때문일 수도 있다.)

- 랜덤이라 그런지 참여가 저조하여 팀 협업이 잘 되지 않은 점이 아쉬웠다

- 논문 구현을 각자 나눠서 진행
- 협업에 대한 방향을 정할 때 학습 파이프라인은 동일하게 구동되는 것을 원칙으로 했다
- 각각 논문 구현을 맡아 진행했을 때 막히는 경우 함께 고민하지 못 해 아쉬웠다.

문종님은 파이프라인을 공유하는 것이 중요하다고 생각하셨는데 결국 중구난방하게 되어 폴더 별로 관리하게 되었다. 협업을 하면서 각 팀원이 가지고 있는 능력을 끌어내기 위해 어떻게 친근해져야 하는지 고민이 필요하다고 생각.

팀에게 기여하지 못 해 스트레스를 받는 경우도 있었다. 기술적인 능력도 중요하지만 소통도 중요하다는 사실을 느꼈다.

팀 분위기가 좋으면 좌절이나 절망을 쉽게 빠져나올 수 있는 장점이 있다. 능력이 극대화할 수 있다고 생각했다.

자신이 어떤 역할을 할 수 있는지 고민이 필요. 기술 능력에 따라 자신의 역할을 잘 찾아가는 생각이 모든 팀원에게 필요.

디버깅에서 작은 부분이 잘못 됐을 때 전체에 영향을 끼치는 걸 보고 꼼꼼히 생각해야 된다는 점을 깨닫게 되었다.

깃헙을 잘 활용하면 공유가 가능하다.

## 멘토링
전체 데이터가 많으면 표본을 추출해서 일부만 학습을 하고 어느정도 성능이 나오면 이후 전체를 학습하는 방법
일부가 전체의 보장이 되지는 않지만 많은 실험이 목표라면 subset이 30에폭에 수렴하면 전체에서도 30에폭에 수렴할지? 데이터셋에 따라 다르다. 소규모\/대규모에 따라 다른 에폭과 관련된 논문을 찾아볼 수도 있다.

분포를 유지해서 작은 크기의 데이터를 만드는 데 분포를 유지하는 기준은? 서브셋을 정확하게 정의내리는 것은 연구자의 역량. 평균적으로 비슷한 길이나 대화의 턴이 몇 번 유지되는지. 고르게 분포되도록 나누는, 여러 방법이 있다.
고전적인 방법으론 계층적 클러스터링
RandomSampling 군집, 통계학에서의 샘플링 기법을 데이터에서 어떻게 찾을 지 고민

잘 알려지지 않은, 대중화되지 않은 task. 나중에는 DST가 stage 1, 2처럼 end-to-end task가 될 수도 있다. DST의 오픈소스가 나올 수 있다.

부스트캠프가 끝나고 회고하는 시간을 갖는 것도 좋다.
