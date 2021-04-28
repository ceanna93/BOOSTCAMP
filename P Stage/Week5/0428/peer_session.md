### Jupyter Notebook 환경에서 학습
args.data_dir = os.environ['SM_CHANNEL_EVAL']
args.model_dir = os.environ['SM_CHANNEL_MODEL']
args.output_dir = os.environ['SM_OUTPUT_DATA_DIR']

환경변수를 직접 변경해줘야 한다.

### Jupyter Notebook terminal에서 실행하면 컴퓨터를 꺼도 실행된다.
tmux 사용해도 kernel이 종료되지 않음

### 내일 논의
- 베이스라인 확인
- 코드
- 학습 속도 향상을 위한 방법
- special mission


### 질문
- CUDA out of memory. Tried to allocate 2.11 GiB (GPU 0; 31.72 GiB total capacity; 28.78 GiB already allocated; 1.64 GiB free; 28.86 GiB reserved in total by PyTorch)
	- 커널 재시작
- from pororo import Pororo
	- version도 상위 버전인데, torch가 여러개 설치되어 있어 그렇지 않을까 추측한다.
