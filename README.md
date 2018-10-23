# bert_language_understanding
Pre-training of Deep Bidirectional Transformers for Language Understanding

This repository is trying to solve some language understanding problems using technology developed in recent years.
 
It is/will be an implement of 'Attention Is All You Need'(Transformer) and 

'Pre-training of Deep Bidirectional Transformers for Language Understanding'. While there is an open source(<a href='https://github.com/tensorflow/tensor2tensor'>tensor2tensor</a>) and official

implementation of Transformer and BERT official implementation coming soon, but there are/may hard to read, not easy to understand. 

We will not try to replicate original papers, but instead to understand and apply main ideas to solve really problem.

## Short Description:
Pretrain mashed language model and next sentence prediction task on large scale of corpus, 

based on multiple layer self-attetion model, then fine tuning by add a classification layer.

As BERT model is based on Transformer, currently we are working on add pretrain task to the model.

<img src="https://github.com/brightmart/bert_language_understanding/blob/master/data/aa3.jpeg"  width="60%" height="60%" />

<img src="https://github.com/brightmart/bert_language_understanding/blob/master/data/aa4.jpeg"  width="65%" height="65%" />

## Usage
to train with transform: python train_transform.py [DONE]

to train with BERT: python train_bert.py [WIP]

## Data Format

input and output is in the same line, each label is start with '__label__'. 

there is a space between input string and the first label, each label is also splitted by a space.

e.g. 
token1 token2 token3 __label__l1 __label__l5 __label__l3
token1 token2 token3 __label__l2 __label__l4

## Pretrain Language Understanding Task

### task 1: masked language model
 
  we feed the input through a deep Transformer encoder and then use the final hidden states corresponding to the masked positions to
    
   predict what word was masked, exactly like we would train a language model.

    source_file each line is a sequence of token, can be a sentence.
    Input Sequence  : The man went to [MASK] store with [MASK] dog
    Target Sequence :                  the                his
    
### task 2: next sentence prediction
  
  many language understanding task, like question answering,inference, need understand relationship
  
  between sentence. however, language model is only able to understand without a sentence. next sentence
  
  prediction is a sample task to help model understand better in these kinds of task.
  
  50% of chance the second sentence is tbe next sentence of the first one, 50% of not the next one.
   
  given two sentence, the model is asked to predict whether the second sentence is real next sentence of 
  
  the first one.
  
    Input : [CLS] the man went to the store [SEP] he bought a gallon of milk [SEP]
    Label : Is Next

    Input = [CLS] the man heading to the store [SEP] penguin [MASK] are flight ##less birds [SEP]
    Label = NotNext
    
for more detail, check method of mask_language_model from pretrain_task.py

<img src="https://github.com/brightmart/bert_language_understanding/blob/master/data/aa1.jpeg"  width="65%" height="65%" />

<img src="https://github.com/brightmart/bert_language_understanding/blob/master/data/aa2.jpeg"  width="65%" height="65%" />


## Environment
python 3+ tensorflow 1.10

## Toy Task

toy task is used to check whether model can work properly without depend on real data.

it ask the model to count numbers, and sum up of all inputs. and a threshold is used, 

if summation is greater(or less) than a threshold, then the model need to predict it as 1( or 0).

inside model/transform_model.py, there is a train and predict method. 

first you can run train() to start training, then run predict() to start prediction using trained model. 

as the model is pretty big, with default hyperparamter(d_model=512, h=8,d_v=d_k=64,num_layer=6), it require lots of data before it can converage.

at least 10k steps is need, before loss become less than 0.1. if you want to train it fast with small

data, you can use small set of hyperparmeter(d_model=128, h=8,d_v=d_k=16, num_layer=6)


## Multi-label Classification Task with transformer and BERT
you can use it two solve binary classification, multi-class classification or multi-label classification problem.

it will print loss during training,  and print f1 score for each epoch during validation.

## Reference
<a href='https://arxiv.org/abs/1706.03762'>Attention Is All You Need</a>

<a href='https://arxiv.org/abs/1810.04805'>BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding</a>



