# 수업
## 1. (Task-Oriented) Dialogue System
### 1.1. Taxonomy of dialogue system
Task-Oriented dialogue & Open-domain dialogue (Chit-Chat)

- Dialogue Coverage: 대화를 커버하는 범위.
- Predefined Scenario

**Task-Oriented dialogue:** Predefined Scenario로 task를 정의하게 되고 특정 태스크를 수행해서 성공하게 만드는 것이 목적

**Open-domain dialogue:** 미리 정의된 시나리오가 없이 대화 주제에 제한이 없다. 인간다움, 자연스러움, 답변의 일관성과 몰입도가 목적이다.

#### DST는 Task-Oriented dialogue
### 1.2 Task-Oriented dialogue: Problem Definition
어떤 정보를 유저와 시스템이 주고 게임. 유저 입장에서 정보는 목적이 정의되고 시스템은 유저가 목적을 달성할 수 있게 도와주는 Knowledge Base에 접근할 수 있다.
특정 task에 성공률을 높이는 것이 시스템의 목적이다.

**Predefined Scenario**
Task Schema(시나리오에서 제공하는 정보를 가지고 있는 DB)를 따르게 된다.

### 1.3 TOD: Task Schema
- Informable Slot: 특정 KB instance를 찾거나 새로운 instance를 write하기 위해 User가 System에게 주거나 맥락에 의해 User가 의도할 수 있는 타입의 정보. 대회 시나리오를 제약하는 사항. (User가 System에게 제공).
- Requestable Slot: informable Slot으로 정보를 찾고 난 이후 추가적으로 검색된 KB instance에 대해 물어보거나 정보를 요청할 수 있는 타입의 정보. (System이 User에게 제공).
- User의 Goal은 위 두 개를 목적으로 한다.

Schema는 정해진 양식을 따르지는 않지만 미리 정의된 시나리오를 slot이라는 정보로 표현하게 된다.

### 1.4 Knowledge Base
시나리오를 성공시키기 위해 시스템이 접근할 수 있는 정보.

정의된 task schema를 따르는 DB. 시스템은 user의 목적을 지속적으로 tracking하면서 DB에 접근해 알맞은 정보를 찾아 답변을 만들어줘야 한다.

### 1.6 Components of Modularized TOD System
DM: NLU에서 추출한 정보로 의사 결정을 내리는 부분
- Dialogue State Tracking
- KB 접근
- Dialogue Policy Optimization

## 2. Dialogue State Tracking
### 2.1 Dialogue State
task schema에 의해 미리 정의된 Informable Slot 타입 J개에 대해 User가 의도하고 있는 Value의 상태를 매 turn마다 tracking해야 되는 상태. 즉 J개의 Slot, Value pair의 set으로 표현.

### 2.2 Evaluation Metrics
- Joint Goal Accuracy: turn t에 시스템이 예측한 dialogue와 ground truth의 dialogue 사이의 exact maching. 매우 어려운 metric
- Slot Accuracy: Dialogue state 간의 비교가 아닌 개별 Slot j의 pair level의 accuracy. Joint Goal에 비하면 관대한 metric.

## 3. Properties of DST
### 3.1 Slot Extraction vs DST
||NLU(sot Extractor)|DST|
|:---:|:---:|:---:|
|Input|Dialogue Context|Dialogue Context, slot value, slot type, ...|
|Model's goal|Extract slot value from the input|Estimate all slot values of Predefined slots|
|Tracking abstractive slot value|X|O|
|Utilizing Ontology|X|O/**X**|
|Handling ASR error|X|O|
|Handling State update|X|O|

### 3.2 DST as Entity Extraction
BIO tags를 사용하여 context에 대해 dialogue state를 파악

Abstractive한 속성을 지니는 Boolean Type의 Slot이나 "dontcare"나 "none"과 같은 Special한 Case를 처리하기 위한 추가적인 후처리가 필요

### Entity Typing & Identification
다르게 표현된 value에 대한 표준화가 필요

### Decision making based on Context
여러 turn에 걸쳐 의사 결정이 이루어지기도 한다.

### State Update
매 turn마다 Slot의 value를 추론.
DST는 value의 변화를 감지해야 하기 때문에 State Update 담당

## Wizard-of-Seoul (WOS)
### 1. Introduction to Wizard-of-Seoul
#### 1.1 Overview
Multi-Domain Dialogue State Tracking

#### 1.3 Data Construction
Wizard-of-Oz framework

System role은 사림인 척하는 system.

Easy-to-Follow Goal Instruction

#### 2.1 DSTEvaluator
None이 포함되기 때문에 Ground Truth와 길이가 다를 수 있다. 길이가 다르더라도 turn slot accuracy의 평가는 0이 아닐 수 있다. 하지만 길이가 다르면 joint goal accuracy는 0이 된다.

--------------------------------------------
# Daily Mission
## 1) WoS의 Domain
**Domain**은 시나리오. Multi-Domain Dialogue State Tracking에 나와있는 것처럼 5가지의 Multi-Domain을 가진 DST 데이터셋.
- 관광
- 숙소
- 식당
- 지하철
- 택시
## 2) WoS의 Slot
**(Informable) Slot**의 개수는 45개. Informable Slot은 User가 System에게 전달하는 정보
Domain별로 어떤 Slot으로 이루어져있는지.

slot_meta.json 파일에 정리

<details>
<summary>Domain 당 Slot</summary>
<div markdown="1">
   
<ul>
<li> 관광
    <ul>
        <li>경치 좋은</li>
        <li>교육적</li>
        <li>도보 가능</li>
        <li>문화 예술</li>
        <li>역사적</li>
        <li>이름</li>
        <li>종류</li>
        <li>주차 가능</li>
        <li>지역</li>
    </ul>
    <li>숙소</li>
    <ul>
        <li>가격대</li>
        <li>도보 가능</li>
        <li>수영장 유무</li>
        <li>스파 유무</li>
        <li>예약 기간</li>
        <li>예약 명수</li>
        <li>예약 요일</li>
        <li>이름</li>
        <li>인터넷 가능</li>
        <li>조식 가능</li>
        <li>종류</li>
        <li>주차 가능</li>
        <li>지역</li>
        <li>헬스장 유무</li>
        <li>흡연 가능</li>
    </ul>
    <li>식당</li>
    <ul>
        <li>가격대</li>
        <li>도보 가능</li>
        <li>야외석 유무</li>
        <li>예약 명수</li>
        <li>예약 시간</li>
        <li>예약 요일</li>
        <li>이름</li>
        <li>인터넷 가능</li>
        <li>종류</li>
        <li>주류 판매</li>
        <li>주차 가능</li>
        <li>지역</li>
        <li>흡연 가능</li>
    </ul>
    <li>지하철</li>
    <ul>
        <li>도착지</li>
        <li>출발 시간</li>
        <li>출발지</li>
    </ul>
    <li>택시</li>
    <ul>
        <li>도착 시간</li>
        <li>도착지</li>
        <li>종류</li>
        <li>출발 시간</li>
        <li>출발지</li>
    </ul>
</ul>

</div>
</details>

## WoS의 Value
**Value**는 2320개.

```
import json

with open("C:/Users/AnnaLee/Desktop/data/train_dataset/ontology.json", "r", encoding='UTF8') as st_json:
    st_python = json.load(st_json)
    sum = 0
    for item in st_python:
        print(f"{item}: {len(st_python[item])}")
        sum += len(st_python[item])
    print(sum)
```

<details>
<summary>Slot 당 Value 개수</summary>
<div markdown="1">

<ul>
<li>관광-경치 좋은: 4</li>
<li>관광-교육적: 4</li>
<li>관광-도보 가능: 4</li>
<li>관광-문화 예술: 4</li>
<li>관광-역사적: 4</li>
<li>관광-이름: 103</li>
<li>관광-종류: 13</li>
<li>관광-주차 가능: 4</li>
<li>관광-지역: 7</li>
<li>숙소-가격대: 5</li>
<li>숙소-도보 가능: 4</li>
<li>숙소-수영장 유무: 4</li>
<li>숙소-스파 유무: 4</li>
<li>숙소-예약 기간: 12</li>
<li>숙소-예약 명수: 12</li>
<li>숙소-예약 요일: 9</li>
<li>숙소-이름: 67</li>
<li>숙소-인터넷 가능: 4</li>
<li>숙소-조식 가능: 4</li>
<li>숙소-종류: 7</li>
<li>숙소-주차 가능: 4</li>
<li>숙소-지역: 7</li>
<li>숙소-헬스장 유무: 4</li>
<li>숙소-흡연 가능: 4</li>
<li>식당-가격대: 5</li>
<li>식당-도보 가능: 4</li>
<li>식당-야외석 유무: 4</li>
<li>식당-예약 명수: 12</li>
<li>식당-예약 시간: 569</li>
<li>식당-예약 요일: 9</li>
<li>식당-이름: 44</li>
<li>식당-인터넷 가능: 4</li>
<li>식당-종류: 10</li>
<li>식당-주류 판매: 4</li>
<li>식당-주차 가능: 4</li>
<li>식당-지역: 7</li>
<li>식당-흡연 가능: 4</li>
<li>지하철-도착지: 60</li>
<li>지하철-출발 시간: 12</li>
<li>지하철-출발지: 60</li>
<li>택시-도착 시간: 190</li>
<li>택시-도착지: 298</li>
<li>택시-종류: 5</li>
<li>택시-출발 시간: 431</li>
<li>택시-출발지: 286</li>
</ul>

</div>
</details>

Slot 당 Value가 어떻게 이루어져있는지 예

관광-경치 좋은
- "none"
- "dontcare"
- "yes"
- "no"

## Bigram / Trigram
### N-gram
n-gram은 n개의 연속적인 단어 나열을 의미합니다. 갖고 있는 코퍼스에서 n개의 단어 뭉치 단위로 끊어서 이를 하나의 토큰으로 간주합니다. 예를 들어서 문장 An adorable little boy is spreading smiles이 있을 때, 각 n에 대해서 n-gram을 전부 구해보면 다음과 같습니다.
- unigrams : an, adorable, little, boy, is, spreading, smiles
- bigrams : an adorable, adorable little, little boy, boy is, is spreading, spreading smiles
- trigrams : an adorable little, adorable little boy, little boy is, boy is spreading, is spreading smiles
- 4-grams : an adorable little boy, adorable little boy is, little boy is spreading, boy is spreading smiles

[train_dials_ngram.txt](https://github.com/ceanna93/BOOSTCAMP/files/6376945/train_dials_ngram.txt)

각 도메인 별 user가 입력한 informable Slot에서 등장하는 bigrams와 trigrams를 추출하여 저장한 파일이다.

너무 길어서 bigram은 100개, trigram은 20개 이상 등장한 경우만 제외하면 아래와 같다.

```
관광
{'서울 중앙에': 320, '중앙에 있는': 108, '서울 서쪽에': 213, '적당한 가격대의': 206, '역사적인 랜드마크를': 111, '안녕하세요. 서울': 518, '서울 동쪽에': 192, '관광지를 찾고': 152, '찾고 있어요.': 155, '서울 남쪽에': 229, '찾고 있는데': 120, '서울 북쪽에': 298, '안녕하세요? 서울': 109, '수 있나요?': 127, '찾고 있습니다.': 126, '북쪽에 있는': 106}
{'서울 동쪽에 있는': 43, '관광지를 찾고 있어요.': 41, '문화 예술을 즐길': 20, '예술을 즐길 수': 21, '즐길 수 있는': 22, '경치가 좋은 공원을': 23, '찾고 있는데 서울': 20, '서울 서쪽에 있는': 37, '알 수 있을까요?': 59, '가능한 곳이 있을까요?': 24, '서울 남쪽에 있는': 63, '관광지를 찾아주세요. 종류는': 21, '예술을 관람하기 좋은': 25, '좋은 관광지를 찾고': 20, '서울 중앙에 있는': 70, '서울 북쪽에 있는': 81, '서울 중앙에 위치한': 28, '찾고 있어요. ': 28, '찾아봐주실 수 있나요?': 20, '괜찮은 곳 좀': 25, '예약 가능한 곳이': 23, '관광지를 찾고 있습니다.': 24, '관광지를 찾고 있는데': 34, '추천해주실 수 있나요?': 25, '경치가 좋은 관광지를': 29, '추천 좀 해주세요.': 22, '있는 적당한 가격대의': 33, '아이들 교육에 좋은': 23}
식당
{'서울 중앙에': 427, '중앙에 있는': 144, '적당한 가격대의': 347, '안녕하세요. 서울': 648, '서울 북쪽에': 314, '주차가 가능한': 113, '찾고 있습니다.': 142, '식당을 찾고': 120, '비싼 가격대의': 115, '서울 동쪽에': 288, '북쪽에 있는': 110, '찾고 있어요.': 173, '찾고 있는데': 168, '서울 남쪽에': 311, '저렴한 가격대의': 112, '좀 찾아주세요.': 124, '서울 서쪽에': 294, '남쪽에 있는': 104, '안녕하세요? 서울': 122, '수 있나요?': 116, '예약 좀': 100}
{'예약 가능한 곳이': 23, '가능한 곳이 있을까요?': 21, '동쪽에 적당한 가격대의': 20, '있는 한식당을 찾고': 22, '서울 북쪽에 있는': 83, '서울 동쪽에 있는': 56, '서울 남쪽에 적당한': 27, '남쪽에 적당한 가격대의': 24, '문화 예술을 즐길': 20, '예술을 즐길 수': 21, '즐길 수 있는': 21, '서울 동쪽에 저렴한': 21, '알 수 있을까요?': 38, '있는 비싼 가격대의': 27, '한식당을 찾고 있습니다.': 22, '서울 중앙에 있는': 100, '위치한 적당한 가격대의': 31, '적당한 가격대의 식당을': 38, '서울 남쪽에 있는': 76, '식당 예약 좀': 21, '서울 중앙에 위치한': 38, '있는 적당한 가격대의': 62, '서울 서쪽에 있는': 50, '괜찮은 곳 좀': 27, '서울 중앙에 적당한': 25, '중앙에 적당한 가격대의': 26, '찾아봐주실 수 있나요?': 25, '숙소를 찾고 있어요.': 20, '식당을 찾고 있는데': 30, '숙소를 찾고 있는데': 27, '식당을 찾고 있어요.': 25, '예약 좀 해주세요.': 25, '찾고 있어요. ': 27, '서울 서쪽에 위치한': 20, '한식당을 찾고 있어요.': 25, '찾고 있는데 서울': 30, '추천해주실 수 있나요?': 24, '남쪽에 있는 비싼': 20, '경치가 좋은 관광지를': 29, '추천 좀 해주세요.': 26, '곳을 찾고 있는데': 20, '아이들 교육에 좋은': 23, '비싼 가격대의 식당을': 24}
지하철
{'안녕하세요. 서울': 128}
{'문화 예술을 즐길': 20, '예술을 즐길 수': 21, '즐길 수 있는': 21, '서울 북쪽에 있는': 26, '서울 중앙에 있는': 22}
택시
{'안녕하세요. 서울': 384, '서울 북쪽에': 155, '서울 중앙에': 226, '서울 남쪽에': 164, '서울 동쪽에': 146, '적당한 가격대의': 115, '좀 찾아주세요.': 106, '서울 서쪽에': 194}
{'가는 택시 좀': 28, '택시 좀 찾아주세요.': 31, '적당한 가격대의 숙소를': 24, '서울 서쪽에 있는': 27, '서울 북쪽에 있는': 32, '예술을 관람하기 좋은': 25, '서울 중앙에 있는': 42, '있는 적당한 가격대의': 27, '서울 동쪽에 있는': 23, '찾고 있어요. ': 20, '서울 남쪽에 있는': 33, '찾아봐주실 수 있나요?': 20}
숙소
{'안녕하세요. 서울': 615, '서울 중앙에': 332, '서울 남쪽에': 315, '저렴한 가격대의': 132, '중앙에 있는': 107, '적당한 가격대의': 344, '가격대의 숙소를': 100, '서울 북쪽에': 272, '서울 동쪽에': 299, '숙소 좀': 116, '좀 찾아주세요.': 114, '숙소를 찾고': 201, '찾고 있는데': 125, '서울 서쪽에': 288, '비싼 가격대의': 151, '찾고 있어요.': 182, '있는 비싼': 100, '안녕하세요? 서울': 126, '찾고 있습니다.': 141, '수 있나요?': 116, '예약 좀': 110}
{'서울 중앙에 위치한': 34, '예약 가능한 곳이': 30, '가능한 곳이 있을까요?': 28, '서울 남쪽에 위치한': 24, '적당한 가격대의 숙소를': 44, '서울 북쪽에 있는': 73, '서울 동쪽에 있는': 51, '서울 남쪽에 적당한': 28, '남쪽에 적당한 가격대의': 32, '숙소 좀 찾아주세요.': 29, '있는 저렴한 가격대의': 21, '서울 중앙에 적당한': 21, '중앙에 적당한 가격대의': 23, '서울 동쪽에 위치한': 26, '서울 동쪽에 저렴한': 28, '숙소를 찾고 있는데': 47, '찾고 있는데 서울': 20, '숙소를 찾고 있어요.': 58, '찾고 있어요. ': 29, '있는 비싼 가격대의': 36, '비싼 가격대의 숙소를': 33, '가격대의 숙소를 찾고있어요': 20, '서울 남쪽에 있는': 65, '알 수 있을까요?': 28, '서울 서쪽에 있는': 43, '가격대의 게스트 하우스를': 20, '적당한 가격대의 호텔을': 40, '서울 중앙에 있는': 67, '예술을 관람하기 좋은': 25, '있는 적당한 가격대의': 57, '예약 좀 해주세요.': 27, '찾아봐주실 수 있나요?': 23, '가격대의 숙소를 찾고': 22, '숙소를 찾고 있습니다.': 31, '서쪽에 적당한 가격대의': 22, '위치한 적당한 가격대의': 37, '적당한 가격대의 에어비엔비를': 20, '괜찮은 곳 좀': 21, '남쪽에 있는 비싼': 22, '숙소 예약 좀': 32, '서울 서쪽에 비싼': 20, '아이들 교육에 좋은': 23, '서울 서쪽에 위치한': 23}
```

추출하기 위한 코드는 아래
```
import json
from collections import defaultdict, Counter

f = open("C:/Users/---/Desktop/data/train_dataset/train_dials_ngram_by_freq.txt", 'w')
with open("C:/Users/---/Desktop/data/train_dataset/train_dials.json", "r", encoding='UTF8') as st_json:
    st_python = json.load(st_json)
    domain_dict = defaultdict(list)
    for item in st_python:
        for domain in item['domains']:
            domain_dict[domain].append(item['dialogue'][0]['text'])
    for domain, texts in domain_dict.items():
        bigram, trigram = [], []
        for text in texts:
            words = text.split(" ")
            for i in range(1, len(words)):
                if i > 2:
                    trigram.append(' '.join(words[i-2:i+1]))
                bigram.append(' '.join(words[i-1:i+1]))
        bi = {x: count for x, count in Counter(bigram).items() if count >= 100}
        tri = {x: count for x, count in Counter(trigram).items() if count >= 20}
        f.write(f"{domain}\n")
        f.write(f"{bi}\n")
        f.write(f"{tri}\n")

f.close()
```

informable slot의 bigram과 trigram을 추출하는 게 어떤 도움이 될 지는 아직이다.
