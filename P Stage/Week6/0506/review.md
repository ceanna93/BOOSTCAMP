## 강의
TRADE 복습

[Transferable Multi-Domain State Generator for Task-Oriented Dialogue Systems](https://arxiv.org/pdf/1905.08743.pdf)

Gate 개수 변경
```
self.gating2id = {"none": 0, "dontcare": 1, "ptr": 2, "yes": 3, "no", 4}
```

#### 질문
I have been reading the early paper on pre-training in NLP (https://arxiv.org/abs/1511.01432) and I can't understand what random word dropout means. The authors completely ignore explaining this method as if it was a standard thing. Can someone explain what they really do and what is the purpose of that?

#### 답변
It is not uncommon that we can make sense of a sentence without reading it completely. Or when you are having a quick look at a document, you tend to oversee some words and still understand the main point. This is the intuition behind the word dropout.

Generally this is done by randomly dropping each word in a sequence following for example a Bernoulli distribution:

<img src="https://user-images.githubusercontent.com/12611645/117306903-0fac4e80-aebb-11eb-83fe-7a43df7bf468.JPG">


where X is the index of the word token, n is the lenth of the sequence, and e⃗  is a vector with each word dropout state.

This is usually done after calculating the word embeddings, and the words selected to be left out are normally changed to the <UNK> equivalent embedding.

By doing this, we allow our model to learn more flexible ways of writing/convey meaning.


## Competition
state가 belief_state

create_data.py 로 생성되는 파일이 train_dials와 비슷한 구조

### 다른 점
create_data.py로 생성된 파일에는 turn마다 domain 값이 존재 (정확하지는 않지만 매 턴마다 사용자의 발화와 관련된 도메인이라고 추정). 해당 domain 정보가 존재하지 않기 때문에 state의 가장 마지막 도메인 값으로 turn\["doamin"\]에 넣어줌.
create_data.py 파일의 getDomain 부분의 반환에서 주석을 보면 아래처럼 적혀있다.

```
return crnt_doms[0] # How about multiple domains in one sentence senario ?
```

하나의 문장에 2개의 도메인이 포함된 경우에 대한 처리가 되어있지 않은 것으로 보인다.

(피어세션을 통해 state가 belief_state라는 사실을 알았다. train_dials를 자세히 봤더라면 다른 분들의 도움 없이 더 빠르게 진행할 수 있었을 텐데 많이 아쉬웠다.)
