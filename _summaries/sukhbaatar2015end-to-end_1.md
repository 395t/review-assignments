---
layout: summary
title: Summary
paper: sukhbaatar2015end-to-end_1
# Please fill out info below
author: DartingMelody
score: 6
---

* What is the core idea?

The paper introduces a novel recurrent neural network with an explicit large memory and a recurrent attention mechanism. The model reads recurrently from memory multiple times before giving the results. This model is trained end-to-end and therefore requires comparitively less supervision during training. Hence, it can also be applied to realistic settings. The paper also shows experimentally that multiple hops over the long-term memory leads to good performance of the model. 

* How is it realized (technically)?

The Model takes as input x1,...,xn (to store in memory), query q and outputs answer a. The model writes all x to the memory up to a fixed buffer size and creates continuous representation of x and q. 

Single layer:

1) The input set{xi} is embedded with matrix A ( d x V) to give memory vectors {mi}. 
2) The query q is also embedded with matrix B (d x V) to give an internal state u.
3) On computing match between each memory mi and u is computed by taking softmax of their inner product which results into the probability vector p over the inputs. 

4) Each xi has a corresponding mapping to an ouput vector ci (using another embedding matrix C).
5) The final output is the sum of the weighted probabilities pi over the transformed input ci. 

6) The output vector o and embedding vector u is added and multiplied by the final weight matrix W which is then passed on to the softmax to predict the output. 

7) As the input to output function is smooth, the gradient an be easily computed of this continuous function. All three embedding matrices A, B, C and weight matrix W are learnt by minimizing cross entrophy loss. 

Multiple layer:

1) For layers above the first layer, the input is the sum of the output o^k and the input u^k. 

2) Each layer has it's own embedding matrices A and C but have constraints to ease training and reduce hyperparameters. 
3) At final layer, the output o is:

Constraints on embedding vectors:

Adjacent:
1) The output embedding for one layer is input embedding for another i.e. A^(k+1) = C^k.
2) The answer prediction matrix is equal to output matrix i.e. W^T = C^k. 
3) The question embedding matches the input embedding of the first layer i.e. B = A^1.

Layer-wise (RNN-like):
1) Same input and output embeddings across different layers i.e. A^1 =A .....A6K. and C^1....C^k. 
2) Add a linear mapping H to update u between hops i.e. u^k+1 = dsakl.
3) H is also a learnable parameter. 

Model details:
1) The question and input sentences are embedded as bag of words. 

2) To capture the position of words within a sentence/questions, position encoding is used.  

3) Some of the QA tasks requires temporal context, hence the memory vector is modified as: 

Both TA and Tc are learning parameters. 
4) Dummy memories are added to regularize Ta which is referred as random noise. 
5) Another variation is not using softmax layer until the validation loss starts decreasing which is referred as linear start training. 

* How well does the paper perform?
The model was tried on various variants like bag of words representation, position encoding representaion, linear start training and random injection of time index noise, RNN-style layer-wise weight tying, adjacent weight tying, joint training on all tasks, per tasks trainings. 
These models were compared with MeMNN, MemNN-WSH, LSTM. All variants of the model beats the weakly supervised baseline models. 
The position encoding representation performs better than bag of words representation especially on tasks where word ordering is important. 
Linear Start helps to avoid local minima. 
Jittering the time index with random empty noises gives small but consistent boost in performance. 
Joint training performs better in all the models.

* What interesting variants are explored?
The model while in operating on a word level was applied on a language modeling task with the following changes:
1) The previous N words in the input sentences are embedded into memory separately.
2) q is a fixed constant vector (without embeddings) as there is no input query.
ReLU is applied to half of the layer. Layer wise RNN weight sharing is used. 
The model closely resembles RNN with the difference that the sequence over which network is recurrent is not in text but in memory hops. One interesting obeservation was some hops concentrate on recent words while other hops have more broad attention span over all memory locations.

The end to end network memory model still lags behind memory networks trained with strong supervision. 


## TL;DR
* Three
* Bullets
* To highlight the core concepts
