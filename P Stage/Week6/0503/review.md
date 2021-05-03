# 강의

## Predefined Ontology-based DST model의 한계
Ontology의 slot-value의 candidate이 존재한다는 가정(모든 value가 ontology 안에 존재한다는 가정)

## Ontology-based DST의 특징
- Ontology = Prioir Knowledge
- Ontology volume에 따른 complexity (Ontology의 domain이 작아야 Classification에 문제가 없는데 최근에 domain이 늘어났고 실제 상황에선 ontology가 훨씬 커진다.)
- Unseen slot value tracking이 어려움(현실에는 Unseen value 존재)

### Prior Knowledge
Ontology에 속한 value 중 하나로 pointing하는 문제로 formulation하기 때문에 학습이 용이하고 쉬운 문제가 될 수 있지만 Set의 크기가 커질수록 scoring과 normalization하는 과정이 어려움

### Unseen Slot Value
Scalable하기 어려움

## Open-Vocab DST model
Decoder(Conditional Language Modeling)을 통해 Value가 등장할 Vocab space에 표현

Ontology의 존재를 가정하지 않는다. => Unseen Value에 대한 tracking이 용이하다.

### Sequicity
sequence 자체를 코딩

### DST-Reader
Generation이 아닌 Extraction으로 문제를 푼다.

#### Extracted한 방법의 한계
- Incorrect Slot Resolution (Identification이 되지 않는다)
- Imprecise Slot Boundary

## TRADE
Open-Vocab 모델

- Utterance Encoder
- State Generator
- Slot Gate Classifier
- Paramter sharing
- Unseen domain evaluation


# Competition
강의의 TRADE Github 페이지에 가보면 [create_data.py](https://github.com/jasonwu0731/trade-dst/blob/master/create_data.py) 파일로 전처리를 해주는 부분이 있다. 약어나 잘못된 맞춤법/오타를 교정해주는데, Wizard-of-Seoul 데이터에도 잘못된 맞춤법이 있다. 이러한 부분을 수정해주면 성능이 개선되지 않을까 생각했지만 잘못된 단어, 맞춤법 등을 어떻게 수정해줘야 하는지가 어렵다. 관련 딥러닝 정보도 대부분 영어로 되어 있다.
