# Competition
### K-Fold
```
from sklearn.model_selection import KFold, StratifiedKFold
import wandb


class CrossValidation:
    """Cross Validation 함수 집합

    """
    def __init__(self, args):
        self.args = args
    def kfold(self, data, shf=True):
        """K-Fold validation

        Arguments:
            data {ndarray} -- 전체 train data
            num {integer} -- K 개수 설정
            shf {boolean} -- 데이터의 Shuffle 여부

        """
        kf = KFold(n_splits=self.args.k_fold_num, shuffle=shf)
        for train_index, valid_index in kf.split(data): 
            t_d = data[train_index]
            v_d = data[valid_index]
            
            wandb.init(project=self.args.wandb_proj_name, config=vars(self.args), reinit=True) 
            trainer.run(args, t_d, v_d)

    def stratified_kfold(self, data, shf=True):
        """K-Fold validation

        Arguments:
            data {ndarray} -- 전체 train data
            num {integer} -- K 개수 설정
            shf {boolean} -- 데이터의 Shuffle 여부

        """
        skf = StratifiedKFold(n_splits=self.args.k_fold_num, shuffle=shf)

def main(args):
    wandb.login()
    
    setSeeds(42) 
    device = "cuda" if torch.cuda.is_available() else "cpu"
    args.device = device

    preprocess = Preprocess(args)
    preprocess.load_train_data(args.file_name)
    train_data = preprocess.get_train_data()

    cv = CrossValidation(args)
    cv.kfold(data=train_data)
```

### Augmentation
```
        df = df.sort_values(by=['userID','Timestamp'], axis=0)
        columns = ['userID', 'assessmentItemID', 'testId', 'answerCode', 'KnowledgeTag']
        group = df[columns].groupby('userID').apply(
                lambda r: (
                    r['testId'].values, 
                    r['assessmentItemID'].values,
                    r['KnowledgeTag'].values,
                    r['answerCode'].values
                )
            )

        aug = group
        idx = 0
        for ft in tqdm(group):
            for split in range(0, len(ft[0]), self.args.max_seq_len-1):
                aug.loc[idx] = tuple([ft[0][split:split+self.args.max_seq_len], ft[1][split:split+self.args.max_seq_len], ft[2][split:split+self.args.max_seq_len], ft[3][split:split+self.args.max_seq_len]])
                idx += 1

        return aug.values
```
