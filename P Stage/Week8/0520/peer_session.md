## 앙상블
- hard voting

## 후처리
- [맞춤법 검사](
https://github.com/ssut/py-hanspell)를 통해 generate에서 잘못 생성된 값을 처리할 수 없는지 확인 => 고유명사 같은 경우 오히려 잘못된 값으로 변경될 수 있음
- cosine_similarity를 이용해 generate에서 잘못 생성된 값이 ontology에 있는지 확인하고 유사한 값이 있다면 해당 값으로 대체 => 성능이 오르지 않음
