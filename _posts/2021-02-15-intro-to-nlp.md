---
title: "Intro to NLP"
date: 2021-02-15 00:18:00 -0400
categories: AI
---

# Intro to Natural Language Processing(NLP)
+ Academic Disciplines related to NLP
+ Treands of NLP

## NLP(Natural Language Processing)
NLU(Natural Language Undestanding)과 LNG(Natural Language Generation이 존재

<img src="https://user-images.githubusercontent.com/12611645/107938878-53cd3880-6fc9-11eb-81e2-fa1a85526400.png" width="40%" height="30%" title="NLP diagram" alt="NLPDiagram">

집합으로 표현하면 [위 그림](https://insights.ai-jobs.net/the-past-and-the-present-of-natural-language-generation/)과 같다.

## Natural language processing
NLP는 최첨단 딥러닝 모델 및 작업을 포함하고 있다.

<span style="color:#D3D3D3">Includes state-of-the-art deep</span>


자연어 처리에서는 다양한 아래를 포함한 다양한 Task를 다루게 된다.
### Low-level parsing
각 단어를 준비하기 위한 가장 low level의 task
+ Tokenization
    + 문장을 이루는 각 단어들을 정보 단위로 생각.
    + 주어진 문장<sup>[1](#footnote_1)</sup>을 단어(Token) 단위로 나누는 과정
+ Stemming
    + 어미 변화에 따른 의미 변화를 없애고 단어의 어근을 추출

### Word and phrase level
+ Named entity recognition(NER<sup>[2](#footnote_2)</sup>)
+ part-of-speech(POS<sup>[3](#footnote_3)</sup>) tagging
+ noun-phrase chunking
+ dependency parsing
+ coreference resolution

### Sentence level
+ Sentiment analysis
    + <span style="color:#A9A9A9">문장의 긍정/부정 판단</span>
+ machine translation
    + <span style="color:#A9A9A9">영어 문장을 한글 문장으로 번역</span>

### Multi-sentence and paragraph level
+ Entailment prediction
    + <span style="color:#A9A9A9">두 문장의 논리적인 내포, 모순 관계 파악</span>
+ question answering
    + <span style="color:#A9A9A9">독해 기반의 질의 응답 (구글 검색에서 문장으로 질문 입력 시 답이 출력)</span>
+ dialog systems
    + <span style="color:#A9A9A9">챗봇 (대화 실행)</span>
+ summarization
    + <span style="color:#A9A9A9">문서 요약</span>

------------------------------------------------------------------
<a name="footnote_1">1</a>: Token들이 특정 순서로 이루어진 sequence
<a name="footnote_2">2</a>: 단일 단어, 고유 단어 인식 task (New york times)
<a name="footnote_3">3</a>: 단어의 품사나 성분을 알아내는 task (주어, 목적어, 동사 등)

