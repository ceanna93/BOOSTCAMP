## SUMBT 학습 제출
pororo를 설치하면 torch의 버전이 강제로 1.6으로 변경되면서 GPU를 사용할 수 없게 되는 문제가 있다. 서버를 다시 할당받아 학습하였다. torch 버전에 따라 torch.div가 사용이 안 될 수 있는 현상이 나타나는 것 같다.

## 자동 제출
```
import json
import requests

def submit(user_key='', file_path = ''):
    if not user_key:
        raise Exception("No UserKey" )
    url = 'http://ec2-13-124-161-225.ap-northeast-2.compute.amazonaws.com:8000/api/v1/competition/25/presigned_url/?description=&hyperparameters={%22training%22:{},%22inference%22:{}}'
    headers = {
        'Authorization': user_key
    }
    res = requests.get(url, headers=headers)
    data = json.loads(res.text)
    
    submit_url = data['url']
    body = {
        'key':'app/Competitions/000025/Users/{}/Submissions/{}/output.csv'.format(str(data['submission']['user']).zfill(8),str(data['submission']['local_id']).zfill(4)),
        'x-amz-algorithm':data['fields']['x-amz-algorithm'],
        'x-amz-credential':data['fields']['x-amz-credential'],
        'x-amz-date':data['fields']['x-amz-date'],
        'policy':data['fields']['policy'],
        'x-amz-signature':data['fields']['x-amz-signature']
    }
    requests.post(url=submit_url, data=body, files={'file': open(file_path, 'rb')})

submit("Bearer 8864ca93a375cf7144b22c16abd14436c6efdd0a", os.path.join(test_dir, 'submission.csv'))
```
위 코드를 사용하여 자동으로 제출했다. 문제는 request 중간에 실패한 경우가 몇 번 있었는데 제출 페이지에서 확인해보니 Create만 되고 Finished가 되지 않은 상태의 파일이 4개가 생성됐다. 서버에 문제가 있지 않길.......

한 가지 불편한 점은 위 방법으로 제출하면 하이퍼 파라미터라든지, 제출한 파일에 대한 설명을 제출 페이지에 추가하지 못 한다는 점이다.
