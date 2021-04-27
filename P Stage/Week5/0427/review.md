# Ontology-based DST models
## 1. Ontology
### 1.1 Classification based DST Recap
Set(S^j)가 Ontology

**Ontology**: 각 Slot j가 가질 수 있는 Value의 후보군을 정의해둔 정보.
모든 Value는 이 안에서만 등장한다고 가정.

일종의 Prior Knowledge로 활용할 수 있다.

Value에 대한 확률적인 표현이 가능.

#### 한계점
- value의 후보군이 많아질수록 더 많은 value를 비교가 필요해 계산 비용이 증가. 특히 Ontogoly가 커졌을 때.
- 현실에서 보지 못 한 데이터 타입이 등장할 확률이 높다. (Unseen Value를 Tracking 하기 까다롭다.

### 2.2 GLAD
GLAD는 많은 수의 모듈을 가지고 있기 때문에 Scaleup을 하기 쉽지 않은 문제가 있다.

### 2.3 GCE
GLAD의 후속 논문
- Slot-Specific Local encoder들을 하나로 Sharing
- Slot dependent encoding
- 하나의 Encoder만 사용하고 Slot dependent한 encoding을 하게 됨
- scoring 모델은 GLAD와 비슷한 구조
encoding을 할 때 관심 있는 slot 타입에 대해 추가적인 토큰을 부여해 utterance들과 같이 encoding을 하게 된다.

## SUMBT
### 3.1 Overview
- Slot, Value와 독립적인 encodings
- Pre-trained LM 인코더 사용

- 두 종류의 BERT 인코더
    - Dialogue Context Encoder
        a. Trun-level hierarchical encoding
        b. Trainable
    - Slot-Value Encoder
        a. Freeze (as Feature extractor)

- Slot-Utterance Matching Module
- GRU based State Tracker
- Non-parametric Scoring (Enclidean)

### 3.2 Encoding Module
BERT를 이용한 Current turn[r_t, u_t] 인코딩

System Response & User Utterance at current turn step

시스템 발화와 사용자 발화를 인코딩
### U_t = BERT([x^{sys}_t, x^{usr}_t])

BERT_sv를 이용한 Slot, Value 인코딩
- [CLS] 토큰을 이용한 Pooling
- 실제론 Freezed encoder를 통해 미리 Ontology 안의 모든 Slot, Value들을 Pre-encoding 후 Lookup

Ontology에 속하는 Slot, Value들을 미리 vector로 만들고 encoder는 빼버린다.

q^s = BERT_{sv}(x^s),
y^v_t = BERT_{sv}(x^v_t).

### 3.3 Slot-Utterance Matching
Multi-head Attention 을 통한 현재 턴 발화들에 대해 Slot s를 Query로 한 Aggregation
- Query: Slot s vector q^s
- Key: Current Turn t encoding U^t
- Value: Current Turn t encoding U^t

=> h^s_t

### 3.4 GRU-based State Contextualizing
GRU를 이용한 현재 Turn에서 Slot s에 대한 State를 Context turns State에 대하여 Contextualize
- Input: h^s_t == Slot s를 Query로 하여 Turn t를 aggregation한 vector
- Output: d^s_t == 이전 Turn (t-1)에서 Slot s에 대한 hidden state와 gating을 통해 update 된 현재 Turn hidden state
- Layer Normalization을 통해 최종 현재 Turn t에서 Slot s에 대한 representation
**\hat{y}^s_t**

### 3.5 Non-Parametric Scoring
Distance function

# Competition
어제 EDA로 ngram 추출하는 작업에서 첫 번째 text에 대해서만 추출하는 문제가 있어 코드를 아래처럼 수정했다.
```
import json
from collections import defaultdict, Counter

f = open("C:/Users/AnnaLee/Desktop/data/train_dataset/train_dials_ngram_by_freq.txt", 'w')
with open("C:/Users/AnnaLee/Desktop/data/train_dataset/train_dials.json", "r", encoding='UTF8') as st_json:
    st_python = json.load(st_json)
    domain_dict = defaultdict(list)
    for item in st_python:
        i = 0
        for domain in item['domains']:
            for dlg in item['dialogue']:
                if dlg['role'] == 'user':
                    domain_dict[domain].append(dlg['text'])
    for domain, texts in domain_dict.items():
        bigram, trigram = [], []
        for text in texts:
            words = text.split(" ")
            for i in range(1, len(words)):
                if i > 2:
                    trigram.append(' '.join(words[i-2:i+1]))
                bigram.append(' '.join(words[i-1:i+1]))

        f.write(f"{domain}\n")
        f.write(f"BIGRAM: {[(l, k) for k, l in sorted([(j, i) for i, j in Counter(bigram).items()], reverse=True)][:10]}\n")
        f.write(f"TRIGRAM: {[(l, k) for k, l in sorted([(j, i) for i, j in Counter(trigram).items()], reverse=True)][:10]}\n")

f.close()
```
결과는 아래와 같다.
```
관광
BIGRAM: [('어떻게 되나요?', 853), ('서울 중앙에', 683), ('서울 북쪽에', 646), ('좀 알려주세요.', 600), ('안녕하세요. 서울', 518), ('수 있나요?', 483), ('같은 지역에', 462), ('저 그리고', 455), ('그리고 서울', 453), ('적당한 가격대의', 444)]
TRIGRAM: [('알 수 있을까요?', 262), ('서울 중앙에 있는', 226), ('같은 지역에 있는', 201), ('서울 북쪽에 있는', 190), ('저 그리고 서울', 131), ('서울 남쪽에 있는', 129), ('감사합니다. 저 그리고', 110), ('서울 동쪽에 있는', 101), ('그리고 서울 중앙에', 100), ('영업 시간이 어떻게', 92)]
식당
BIGRAM: [('서울 중앙에', 775), ('어떻게 되나요?', 681), ('적당한 가격대의', 672), ('안녕하세요. 서울', 648), ('좀 알려주세요.', 646), ('서울 북쪽에', 629), ('서울 남쪽에', 537), ('서울 서쪽에', 521), ('저 그리고', 490), ('서울 동쪽에', 487)]
TRIGRAM: [('서울 중앙에 있는', 253), ('같은 지역에 있는', 233), ('알 수 있을까요?', 203), ('서울 북쪽에 있는', 185), ('서울 남쪽에 있는', 150), ('저 그리고 서울', 136), ('예약 해 주세요.', 130), ('서울 동쪽에 있는', 129), ('예약 좀 해주세요.', 128), ('있는 적당한 가격대의', 127)]
지하철
BIGRAM: [('어떻게 되나요?', 156), ('서울 북쪽에', 131), ('안녕하세요. 서울', 128), ('서울 중앙에', 128), ('수 있는', 111), ('가는 지하철을', 98), ('가까운 지하철역이', 97), ('알아봐 주세요.', 96), ('알아봐주세요. ', 91), ('적당한 가격대의', 85)]
TRIGRAM: [('예술을 즐길 수', 53), ('즐길 수 있는', 49), ('문화 예술을 즐길', 48), ('서울 북쪽에 있는', 44), ('서울 중앙에 있는', 41), ('근처 역은 어디인가요?', 28), ('근처 역으로 가는', 27), ('역사적으로 의미가 있는', 25), ('걸어갈 수 있는', 24), ('지하철역이 어떻게 되나요?', 23)]
택시
BIGRAM: [('좀 알려주세요.', 411), ('안녕하세요. 서울', 384), ('어떻게 되나요?', 372), ('서울 중앙에', 333), ('수 있나요?', 296), ('택시 종류는', 289), ('저 그리고', 289), ('가는 택시를', 264), ('네 감사합니다.', 255), ('서울 서쪽에', 253)]
TRIGRAM: [('알 수 있을까요?', 151), ('서울 중앙에 있는', 90), ('갈 수 있는', 84), ('예약 해 주세요.', 83), ('전화번호 좀 알려주세요.', 79), ('감사합니다. 저 그리고', 74), ('알 수 있나요?', 73), ('저 그리고 택시를', 67), ('될 것 같아요.', 66), ('서울 북쪽에 있는', 60)]
숙소
BIGRAM: [('적당한 가격대의', 677), ('서울 중앙에', 662), ('어떻게 되나요?', 628), ('안녕하세요. 서울', 615), ('좀 알려주세요.', 585), ('서울 북쪽에', 579), ('서울 남쪽에', 538), ('서울 서쪽에', 520), ('서울 동쪽에', 506), ('저 그리고', 482)]
TRIGRAM: [('알 수 있을까요?', 212), ('서울 중앙에 있는', 209), ('같은 지역에 있는', 203), ('서울 북쪽에 있는', 161), ('예약 해 주세요.', 150), ('서울 남쪽에 있는', 133), ('저 그리고 서울', 127), ('예약 좀 해주세요.', 127), ('있는 적당한 가격대의', 121), ('서울 동쪽에 있는', 118)]
```
한 가지 추가로 해보고 싶은 게 slot은 있지만 value에 없는 text가 존재하는지 확인하고 싶었다. 예를 들어 가격대가 문장에 들어가지만 "저렴", "비싼", "적당"이 들어가지 않는 문장이 있다면 출력하고 싶었다. 특히 "비싼"은 "비싸더라도", "비싸지만" 등 다양하게 바뀔 수 있기 때문에 이에 대한 처리를 어떻게 해주어야 할 지 의문이 들었다.

+ ner이나 BIO를 활용할 방법은 없을까.

### SUMBT 정리

