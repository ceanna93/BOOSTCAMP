## 질문
1. entity embedding을 어떻게 넣는지. 베이스라인에 entity embedding을 추가하는 방법은 없는지.


2. R-BERT를 사용했을 때 성능이 떨어지는 이유
    - 이미 BERT에서 사용하는 토큰을 그대로 사용했기 때문으로 예상('$'와 '#'은 이미 BERT에서 사용 중인 토큰이기 때문에 monologg 깃헙에 작성된 코드를 그대로 사용하면 안 된다)

3. 하이퍼 파라미터를 변경했을 때 큰 효과가 있는지
    - max_length와 batch size를 키웠을 때 성능이 향상됐다.

4. pororo의 ner이 tokenizer?
    - ner은 개체 판단 추출을 하는 것으로 tokenizer와는 다르다.
    - 엔티티들이 어떤 개체인지 판단

    + mecab을 이용하여 명사인지 판단하는 건 어떨까?
        - 학습과 추론 데이터의 대부분은 이미 명사라고 생각한다.

## 공유
1. 학습에서 중복되는 문장이 있을 떄 성능이 오히려 떨어진다.
    - 동일한 문장에 entity의 위치들을 바꿔서 학습을 시켰을 때 성능이 떨어진다. (반대되는 라벨이나 동일한 라벨의 경우 위치 변경이 가능하다고 생각해 적용하여 augmentation을 시도했지만 오히려 성능 하락)
    - 학습 데이터에서 중복되는 문장을 제거 했을 때 정확도가 1% 정도 향상됐다.
2. R-BERT를 사용했는데 베이스라인보다 성능이 떨어진다.
3. R-BERT에 KoELECTRA 사용은 가능하다.
    - 성능은 bert-base-multilingual-cased를 사용했을 때보다 떨어진다.
4. R-BERT에서 --max_seq_len 파라미터를 변경하면 학습이 되지 않는다.
    - 문장 길이가 더 길어 문장이 잘리면서 토큰이 분리되기 때문이라고 추측한다.


## 정보
1. KoBERT는 AutoTokenizer를 사용하면 안 되는 경우가 있다.
2. Transformer 버전 확인이 필요하다.
3. [roberta-large](https://huggingface.co/roberta-large)의 경우 UNK 토큰이 없다.

## 기타
1. 서버 용량 확인하는 방법
    cd /opt
    - du -h --max-depth=1 | sort -hr

    => 확인한 결과 현재 31G 사용
