# 강의
## 목표
sequence데이터가 어떻게 주어지더라도 모델링을 할 수 있는 능력을 키우는 것이 목표
1. CFG class를 통해 전체 configuration을 관리
2. feature가 수치형인지 범주형인지 파악하고 이를 embedidng하는 방법을 파악(shape이 어떻게 변하는지)

## Competition
문제를 푼 개수를 feature에 추가한다면?

사용자마다 몇 문제를 풀었는지 EDA
```
plt.hist([len(x[1]['answerCode']) for x in stu_score_groupby])
plt.show()
```

<img src="https://user-images.githubusercontent.com/12611645/119823105-6394db00-bf2f-11eb-9a05-4eea27ae0352.png" width="500"/>

x축이 푼 문제의 수, y축이 사용자의 수
