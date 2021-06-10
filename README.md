# papago
data 폴더에 `train_source.txt`, `train_target.txt`,`test_source.txt`, `test_target.txt` 파일을 업로드 해주세요.
colab pro 기반으로 작성되었으며, pytorch.org/tutorial code를 참고하였습니다. 
```python
from google.colab import drive #edit
drive.mount('/content/drive')
%cd /content/drive/MyDrive/NAVER 
```
의 %cd 부분을 git clone 경로로 바꾸어주세요.


## ipynb file discription
+ GRU.ipynb : GRU model code for predicting target vector. Model includes one encoderRNN and one AttentionDecoderRNN.
    This code saves model in directory model/ with epoch number information. `encoder_{OPTIM}.pth`,`decoder_{OPTIM}.pth`
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



#### Transformer epoch train loss
![Transformer_100](https://user-images.githubusercontent.com/69630288/121541176-05ddb400-ca42-11eb-94e7-8a6fae2e5321.png)

### evaluation
'>' : source
'=' : target
'<' : prediction

Transformer _ epoch 100
<img width="975" alt="스크린샷 2021-06-10 오후 11 32 49" src="https://user-images.githubusercontent.com/69630288/121543856-37577f00-ca44-11eb-8361-3399a9fdeb18.png">


### experiment

#### GRU vs Transformer
|model|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|GRU|177|200|300|
|Transformer|0.246|0.644|0.5025|

#### EPOCHS
##### Transformer
|EPOCHS|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|16|0.0|0.0|0.0|
|40|0.0|0.0|0.496|
|64|0.0|0.0|0.511|
|100|0.246|0.644|0.5025|

#### Optimizer 
##### GRU
|Optimizer|Truely corrected target sequence|Widely corrected target sequence|vector item level accuracy|
|------|---|---|---|
|SGD|0|0|0|
|Adam|0|0|0|

## reference
https://pytorch.org/tutorials/beginner/translation_transformer.html
