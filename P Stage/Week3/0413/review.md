## 강의 내용 정리
### 자연어 전처리
- konlpy
- mecab
- hgtk
- transformers

## Daily Misson
Python을 이용한 방법과 정규식을 이용한 방법의 차이

<pre><code>
text = "슈가 민윤기 1993-03-09 Yunki_INTP@daum.com"
</code></pre>

위 텍스트를 분리할 때 아래 두 가지 방법이 가능
1. text.split(' ')
2. re.findall('([가-힣a-zA-Z]+)\s([가-힣]{2,4})\s([0-9]{4})-([0-9]{2})-([0-9]{2})\s([\w_-]+)@.+\.\w+', text)[0]   (진영기님이 공유해주신 정규식)

[Python extract pattern matches](https://stackoverflow.com/questions/15340582/python-extract-pattern-matches)

두 실행의 차이점은?
2번 방법을 사용할 경우 tuple이 반환된다.
