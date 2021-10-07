---
layout: summary
title: Summary
paper: zaheer2021big
# Please fill out info below
author: biofizzatreya
score: 8
---

TODO: Summarize the paper:
Transformers changed NLP because they are capable of using the attention mechanism. Where an entire sequence is converted into an attention matrix. This allows the network to see the entire sequence simultaneously. Thus the network can infer long-range correlations, which is otherwise difficult for linear models such as LSTM or RNN.  However creating the attention matrix is memory intensive, which restricts the use of transformers on longer sequences. Big-bird attempts to circumvent this challenge by using sparse-attention.

![image](https://user-images.githubusercontent.com/13065170/135767499-1f21fc47-ba6c-402f-bf1e-a1fe6730466b.png)

Instead of a full attention matrix, BigBird uses a mixture of:
* Random attention
* Window attention and
* Global attention

 In BigBird, attention is modelled as a directed graph where,

 $$ \text{ATTN}_D(X)_i = x_i + \sum_{h=1}^H \sigma \left( Q_h(x_i)K_h(X_{N(i)})^T\right)\cdot V_h(X_{N(i)}) $$

$$ Q_h $$ and $$ K_h $$ are query and key functions respectively. $$ V_h $$ is a value function, $$ \sigma $$ is a scoring function and $$ H $$ is the number of heads. The BigBird attention mechanism is tested on a number of datasets.

![image](https://user-images.githubusercontent.com/13065170/135767478-0afa6662-63f2-4352-8253-cb33da39728a.png)


BigBird performs better than models such as RoBERTa and Longformer when it comes to QA type tasks. BigBird also performs better in classification tasks, compared to BERT especially for longer documents. This is presumably because BERT itself starts failing on longer documents.

![image](https://user-images.githubusercontent.com/13065170/135767425-ca4965ae-382d-4177-8004-29e96666e729.png)

The authors tested BigBird on genomic sequences as well. Here BigBird outperforms currently available networks, especially in Promoter Region prediction.




## TL;DR
* Attention memory intensive
* Sparse attention in BigBird
* Works better on longer sequences
