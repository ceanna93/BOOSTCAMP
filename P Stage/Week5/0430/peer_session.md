https://pytorch.org/docs/stable/amp.html
```
import torch.cuda.amp as amp


with amp.autocast():
            output = model(x)
            loss = criterion(output, y)
```

SOTA 모델

test와 train 데이터셋의 분포가 달라 점수가 20 이상 차이가 나고 차가 줄어들지 않는다.

도메인 별 비율로 학습

BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension
- Encoder - BERT
- Decoder - GPT

state-of-the-art

slot, null 추가

tokenize 쪽에서 vocab을 받아와 pretrained된 값을 사용.

책 추천
- 밑바닥부터 시작하는 딥러닝
- 파이썬 날코딩으로 알고 짜는 딥러닝
