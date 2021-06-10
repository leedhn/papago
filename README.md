# papago
data 폴더에 `train_source.txt`, `train_target.txt`,`test_source.txt`, `test_target.txt` 파일을 업로드 해주세요.
colab pro 기반으로 작성되었으며, pytorch.org/tutorial code를 참고하였습니다. 

## ipynb file discription
+ GRU.ipynb : GRU model code for predicting target vector. Model includes one encoderRNN and one AttentionDecoderRNN.
    This code saves model in directory model/ with epoch number information. `encoder_{EPOCH}.pth`,`decoder_{EPOCH}.pth`
    This code saves logfile for recording train loss

+ transformer.ipynb : Transformer model code for predicting target vector. Model includes one transformer.
    This code saves model in directory model/ with epoch number information. `transformer_{EPOCH}.pth`
    This code saves logfile for recording train loss

+ evaluate.ipynb : comparing accuracy with trained models which saved at /trained_models/ dir. 
  + target level accuracy
    + 'Truely corrected target sequence' score: which means model predicted exactly same as target.
    + 'Widely corrected target sequence' score: which means model predicted same as target for corresponding target length, and appended some more values after target length.
  + vector item level accuracy
    + when model predicted exactly same as target, the accuracy is 1.
    + For each index, add 1 if the values are the same, 0 if they are different, and then divide by the final length to get the accuracy.


## task discription

The objective of this task is to create a model that approximates a mapping function from an input sequence of integers ("source") to an output sequence of integers ("target") using a training data set (`train_source.txt`, `train_target.txt`), and achieve best generalization performance on a held-out test set (`test_source.txt`, `test_target.txt`). Use any technique and framework you think is appropriate. 

Please submit a link to a GitHub repository, containing your code, and `README` which describes the following:

1. your experiment design (including baselines and models and/or data exploration results)
2. evaluation metrics
3. experimental results.

## Experiment design

### Baseline/models

GRU, Transformer

### Data Processing

txt 형태의 데이터를 torch.Tensor형태로 변환합니다. 

### Data Loader 

각 모델에 맞게 DataLoader로 배치를 만듭니다. 

### evaluation
'''
something
'''

### experiment

#### GRU vs Transformer
|model|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|GRU|177|200|300|
|Transformer|177|200|300|

#### EPOCHS
##### Transformer
|EPOCHS|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|16|0.0|0.0|0.0|
|40|0.0|0.0|0.496|
|64|0.0|0.0|0.0|
|100|0.0|0.0|0.0|

#### Optimizer 
##### GRU
|Optimizer|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|SGD|0|0|0|
|Adam|0|0|0|

## reference
https://pytorch.org/tutorials/beginner/translation_transformer.html
