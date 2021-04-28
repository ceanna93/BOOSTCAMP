## Special Mission 1: SUMBT 구현하기
1. SUMBTPreprocessor
  TODO 코드
  ```
  label_idx = self.ontology[slot_type].index(value)
  
  def recover_state(self, pred_slots, num_turn):
    states = []
    # TODO
    for pred_slot in pred_slots[:num_turn]:
        state = []
        for s, p in zip(self.slot_meta, pred_slot):
            v = ontology[s][p]
            if v != 'none':
                state.append(f'{s}-{v}')
        states.append(state)
    return states
  ```
2. tokenize_ontology
  TODO 코드
  ```
  def tokenize_ontology(ontology, tokenizer, max_seq_length=12):
    # TODO
    slot_types, slot_values = [], []
    for k, v in ontology.items():
        tokens = tokenizer.encode(k)
        if len(tokens) < max_seq_length:
            gap = max_seq_length - len(tokens)
            tokens.extend([tokenizer.pad_token_id] * gap)
        slot_types.append(tokens)
        slot_value = []
        for vv in v:
            tokens = tokenizer.encode(vv)
            if len(tokens) < max_seq_length:
                gap = max_seq_length - len(tokens)
                tokens.extend([tokenizer.pad_token_id] * gap)
            slot_value.append(tokens)
        slot_values.append(torch.LongTensor(slot_value))
        
    return torch.LongTensor(slot_types), slot_values
  ```
3. inference 함수
  ```
  def inference(model, eval_loader, processor, device):
    model.eval()
    predictions = {}
    # TODO
    for step, batch in enumerate(eval_loader):
        input_ids, segment_ids, input_masks, target_ids, num_turns, guids  = \
        [b.to(device) if not isinstance(b, list) else b for b in batch]

        if n_gpu == 1:
            loss, loss_slot, acc, acc_slot, _ = model(input_ids, segment_ids, input_masks, target_ids, n_gpu)
        else:
            loss, _, acc, acc_slot, _ = model(input_ids, segment_ids, input_masks, target_ids, n_gpu)
            
        predictions[guids] = processor.recover_state(acc_slot, num_turns)
    return predictions
  ```
  predictions는 dict 타입으로 return 해서 \_evalution 함수에서 dev_labels에 들어있는 key 값으로 접근하게 된다. 
  dev_labels에는 아래와 같은 값이 들어있다.
  ```
  {'autumn-mountain-9993:식당_관광_지하철_14-0': ['식당-가격대-적당',
  '식당-지역-dontcare',
  '식당-종류-양식당'],
 'autumn-mountain-9993:식당_관광_지하철_14-1': ['식당-가격대-적당',
  '식당-지역-dontcare',
  '식당-종류-양식당',
  '식당-예약 요일-금요일',
  '식당-예약 시간-03:30',
  '식당-예약 명수-4',
  '식당-이름-어차피자'],  ...(생략)
  ```
  dev_labels에 들어있는 key값을 predictions에 넣어줘야 한다.
  dev_loader를 할당하는 부분을 살펴보면 ```dev_loader = DataLoader(dev_data, batch_size=8, sampler=dev_sampler, collate_fn=processor.collate_fn)```로 되어 있다. 
  collate_fn에는 guid가 들어가있고 이 guid가 dev_labels의 key값과 동일하다. batch에서 값을 가져오는 부분을 보면 guids가 있기 때문에 predictions\[guids\]에 recover_state한 값을 사용해줬다. 학습하는 데 시간이 오래 걸려서 결과를 확인하지 못 하고 있다.
