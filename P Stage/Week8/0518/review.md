## Competition
```
[30/30] [0/1318] mean_loss : 0.162, state_loss : 0.111, gen_loss : 0.051, dom_loss : 0.000
[30/30] [100/1318] mean_loss : 0.185, state_loss : 0.034, gen_loss : 0.042, dom_loss : 0.000
[30/30] [200/1318] mean_loss : 0.186, state_loss : 0.045, gen_loss : 0.068, dom_loss : 0.000
[30/30] [300/1318] mean_loss : 0.172, state_loss : 0.042, gen_loss : 0.049, dom_loss : 0.000
[30/30] [400/1318] mean_loss : 0.175, state_loss : 0.046, gen_loss : 0.165, dom_loss : 0.000
[30/30] [500/1318] mean_loss : 0.179, state_loss : 0.050, gen_loss : 0.123, dom_loss : 0.000
[30/30] [600/1318] mean_loss : 0.173, state_loss : 0.067, gen_loss : 0.158, dom_loss : 0.000
[30/30] [700/1318] mean_loss : 0.188, state_loss : 0.064, gen_loss : 0.055, dom_loss : 0.000
[30/30] [800/1318] mean_loss : 0.175, state_loss : 0.065, gen_loss : 0.169, dom_loss : 0.000
[30/30] [900/1318] mean_loss : 0.173, state_loss : 0.036, gen_loss : 0.109, dom_loss : 0.000
[30/30] [1000/1318] mean_loss : 0.165, state_loss : 0.037, gen_loss : 0.266, dom_loss : 0.000
[30/30] [1100/1318] mean_loss : 0.164, state_loss : 0.055, gen_loss : 0.226, dom_loss : 0.000
[30/30] [1200/1318] mean_loss : 0.178, state_loss : 0.022, gen_loss : 0.101, dom_loss : 0.000
[30/30] [1300/1318] mean_loss : 0.168, state_loss : 0.050, gen_loss : 0.099, dom_loss : 0.000
------------------------------
op_code: 6, is_gt_op: False, is_gt_p_state: False, is_gt_gen: False
Epoch 30 joint accuracy :  0.5426101777453128
Epoch 30 slot turn accuracy :  0.9805670535400574
Epoch 30 slot turn F1:  0.9081757832965781
Epoch 30 op accuracy :  0.9809052295539094
Epoch 30 op F1 :  {'delete': 0.010731707317073172, 'update': 0.8347920238202652, 'dontcare': 0.7506932190572221, 'carryover': 0.9902283255794921, 'yes': 0.7962633451957295, 'no': 0.6351351351351352}
Epoch 30 op hit count :  {'delete': 11, 'update': 9252, 'dontcare': 1489, 'carryover': 350878, 'yes': 895, 'no': 47}
Epoch 30 op all count :  {'delete': 2023, 'update': 11872, 'dontcare': 1876, 'carryover': 352723, 'yes': 1054, 'no': 82}
Final Joint Accuracy :  0.4201091192517537
Final slot turn F1 :  0.8818430792192615
Latency Per Prediction : 23.959149 ms
-----------------------------

숙소 0.652127659574468 0.9871040189125257
지하철 0.042328042328042326 0.961199294532626
식당 0.6760089686098655 0.9898667164922729
관광 0.7815126050420168 0.9941409897292239
택시 0.3089080459770115 0.9725734355044705
Best Score :  {'epoch': 30, 'joint_acc': 0.5426101777453128, 'slot_acc': 0.9805670535400574, 'slot_f1': 0.9081757832965781, 'op_acc': 0.9809052295539094, 'op_f1': {'delete': 0.010731707317073172, 'update': 0.8347920238202652, 'dontcare': 0.7506932190572221, 'carryover': 0.9902283255794921, 'yes': 0.7962633451957295, 'no': 0.6351351351351352}, 'final_slot_f1': 0.8818430792192615}
```

CrossEntropyLoss에 weight을 줘 학습시켰더니 joint accuracy가 어느 정도 올랐다. 처음엔 joint accuracy가 0으로 출력되고 45개의 slot에 대해 전부 generate을 해 시간도 오래 걸렸지만 학습하면 할수록 시간도 줄어들고 accuracy도 오른다.

위는 18 epoch 정도 돌렸다가 터미널을 닫아버려 해당 모델을 다시 불러와 처음부터 30 epoch까지 돌렸을 때의 결과.

결과에 yes, no가 포함된 경우가 많아 op_code를 6으로 학습시켰다.

비교를 위해 아래 5 epoch 학습 결과를 추가
```
[5/30] [0/1318] mean_loss : 1.113, state_loss : 0.389, gen_loss : 0.722, dom_loss : 0.002
[5/30] [100/1318] mean_loss : 1.014, state_loss : 0.373, gen_loss : 0.469, dom_loss : 0.001
[5/30] [200/1318] mean_loss : 1.036, state_loss : 0.253, gen_loss : 0.855, dom_loss : 0.001
[5/30] [300/1318] mean_loss : 1.107, state_loss : 0.284, gen_loss : 0.529, dom_loss : 0.017
[5/30] [400/1318] mean_loss : 1.053, state_loss : 0.628, gen_loss : 0.438, dom_loss : 0.256
[5/30] [500/1318] mean_loss : 1.149, state_loss : 0.371, gen_loss : 0.367, dom_loss : 0.023
[5/30] [600/1318] mean_loss : 1.071, state_loss : 0.370, gen_loss : 0.635, dom_loss : 0.011
[5/30] [700/1318] mean_loss : 1.040, state_loss : 0.282, gen_loss : 0.352, dom_loss : 0.005
[5/30] [800/1318] mean_loss : 1.085, state_loss : 0.538, gen_loss : 0.770, dom_loss : 0.000
[5/30] [900/1318] mean_loss : 1.031, state_loss : 0.433, gen_loss : 0.536, dom_loss : 0.026
[5/30] [1000/1318] mean_loss : 1.068, state_loss : 0.414, gen_loss : 0.574, dom_loss : 0.001
[5/30] [1100/1318] mean_loss : 1.068, state_loss : 0.422, gen_loss : 0.748, dom_loss : 0.138
[5/30] [1200/1318] mean_loss : 1.143, state_loss : 0.481, gen_loss : 0.666, dom_loss : 0.011
[5/30] [1300/1318] mean_loss : 1.036, state_loss : 0.434, gen_loss : 0.413, dom_loss : 0.001
------------------------------
op_code: 6, is_gt_op: False, is_gt_p_state: False, is_gt_gen: False
Epoch 5 joint accuracy :  0.00024348672997321646
Epoch 5 slot turn accuracy :  0.7721072423775153
Epoch 5 slot turn F1:  0.37569298236677956
Epoch 5 op accuracy :  0.7809160511863286
Epoch 5 op F1 :  {'delete': 0.0008893029558736343, 'update': 0.41593013689961394, 'dontcare': 0.3397796817625459, 'carryover': 0.8789695179783082, 'yes': 0.2125632628758559, 'no': 0.2323943661971831}
Epoch 5 op hit count :  {'delete': 21, 'update': 9859, 'dontcare': 1388, 'carryover': 276635, 'yes': 714, 'no': 33}
Epoch 5 op all count :  {'delete': 47197, 'update': 24810, 'dontcare': 2913, 'carryover': 291685, 'yes': 2862, 'no': 163}
Final Joint Accuracy :  0.0
Final slot turn F1 :  0.3650836220608167
Latency Per Prediction : 36.750477 ms
-----------------------------

숙소 0.0015957446808510637 0.8363475177304862
지하철 0.0 0.9476778365667236
식당 0.0016816143497757848 0.8468858993522632
관광 0.0014005602240896359 0.8843215063803163
택시 0.0 0.9196998722860796
Best Score :  {'epoch': 1, 'joint_acc': 0.03274896518139762, 'slot_acc': 0.8705272840408217, 'slot_f1': 0.5543282345951501, 'op_acc': 0.8778589400211254, 'op_f1': {'delete': 0.002060101213668324, 'update': 0.5056048451362695, 'dontcare': 0.4984530766586456, 'carryover': 0.9347327816277557, 'yes': 0.3905893101873002, 'no': 0.3700787401574803}, 'final_slot_f1': 0.5129748413025548}
```
