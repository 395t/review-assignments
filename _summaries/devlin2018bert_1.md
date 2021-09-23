---
layout: summary
title: Summary
paper: {{paper_tag}}
# Please fill out info below
author:  dalmeraz
score: 10
---

TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?


### BERT: Bidirection Encoder Representation from Transormers
BERT is a simple and emprically powerful model that achieves state of the art results in a variety of both token and sentence level tasks. Its smplicity comes from only minimal changes needed to be done to use the model is seperate tasks and its strength comes from its ability to look at text bidirectionally and pre-training. BERT is pre-trained and is then fine-tuned to a variety of tasks.

<p align="center"> <img src="devlin2018bert_1_a.png" height="300"/> </p>


### BERT Architecture
BERT is a multi-layer bidirectional Transformer encoder designed almost identically to the "Attention is all you need" paper. Additionally, BERT is presented in two different sizes, BERT base and BERT Large. The differences for these models can be seen in the following table.

|                      | BASE | LARGE |
|----------------------|------|-------|
| Layers               | 12   | 24    |
| Hidden Size          | 768  | 1024  |
| Self Attention Heads | 16   | 16    |
| Total Parameters     | 110M | 340M  |

Input in BERT is designed to be flexibile to the variety of tasks it would handle. 

<p align="center"> <img src="devlin2018bert_1_b.png" height="300"/> </p>

First, sentences are tokenized via WordPiece. Next, the first token of every sequence is '[CLS]' and if two senteces are to be passed they should be seperated by a token '[SEP]'. Next, embeddings are generates. In addition to generating the token embeddings, the model also generates segment embeddings and position embeddings. Segment refers to what sentence the current token is a part of (so if we're doing a two sentence task, there is two options, if were doing a single sentence task there is only one). Position is the index of the current token. Segment and Position are then embeded and added to the token embeddings. The models output is the same shape as the input and the value of the '[CLS]' token is used for classification tasks.


### Pre-training
BERT is pre-trained through the use of unlabeled data in 2 seperate tasks: Masked Language Modeling (MLM) and Next Sentence Prediction (NSP).

The MLM pretraining task is what allows the model to be bidrectional. Typically, language modeling is done either left to right or right to left since doing bidirectional would allow other parts of the sequence to be seen. However BERT solves this by masking certain tokens and making those the tokens to be predicted. 15% of sequence tokens are masked and the model predicts the masked tokens. Key issue with this is that when fine-tuning the model does not recieve '[MASK]' tokens as input, so to mitigates this, 80% of the time the actual '[mask]' token is used, 10% of the a random token, and 10% the original.

The NSP task was motivated by tasks such as question answering and natural language inference where it is crucial for the model to understand the relationship between two sentences. NSP is a binary predicition task in which two sentncens are given and the model predicts if the second sentence follows the first.

### Fine-tuning
Fine tuning BERT is relatively straight forward, input and output are passed into bert and all parameters are finetuned. For token classification tasks we use outputed tokens, for sentence classification tasks we use the output of the '[CLS]' token, and we can pass two sentences as input by seperating with the '[sep]' token.

## Experiments
For the first set of experiments, BERT used the General Language Understading benchmark (GLUE).

<p align="center"> <img src="devlin2018bert_1_c.png" height="300"/> </p>

BERT large achieves a 7% improvement over the previous SOTA  in the benchmark and 11.1% improvemnt over the best non transofrmer model.

The second set of expermined were done on the Stanford Question Answering Dataset (SQuAD v1.1) in which a question and context is given as input. The model then predicts the span of text that contains the answer. TriviaQA is a seperate dataset that the model was first fine tuned on to  get top  results.

<p align="center"> <img src="devlin2018bert_1_d.png" height="300"/> </p>

Third experiment, SQuAD 2.0, extended SQuAD 1.1 by allowing the possibility for  simple answers to not exist within the context.

<p align="center"> <img src="devlin2018bert_1_e.png" height="300"/> </p>

The fourth task was Situations With Adverserial Generations (SWAG) in which the task is that given 1 sentence, pick which of 4 sentences is a more likely continuation. This is fed to the model as 4 seperate inputs and best result is given as the answer.

<p align="center"> <img src="devlin2018bert_1_f.png" height="300"/> </p>

The next experiments studied the effect of pre-training tasks on different metrics. LTR refers to using left to right LM as opposed to MLM.

<p align="center"> <img src="devlin2018bert_1_g.png" height="300"/> </p>

Finally, the final experiments looks at the effects of different model  sizes on results. One key point to note is generally, the sizes picked for BERT are considerably larger than all other transformers trained previously.

<p align="center"> <img src="devlin2018bert_1_i.png" height="300"/> </p>

## TL;DR
* Bidirecional pre-training is important to generating good models
* Generalized pre-trained representations reduce dependencies on complex models for specific tasks
* Above mentioned points allow for SOTA results on 11 NLP tasks
