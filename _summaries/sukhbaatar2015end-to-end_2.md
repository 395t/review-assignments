---
layout: summary
title: Summary
paper: {{sukhbaatar2015end-to-end}}
# Please fill out info below
author: mmcinnestaylor # Your GitHub id
score: 8 # How did you like this paper 0(dislike) to 10(love)
---

## Core Idea
* End-To-End Memory Networks are a type of Memory Network with a possibly large external memory which is trained end-to-end.
* End-to-end training requires less supervision, thus improving applicability in real world settings.

## Technical Implementation
* The model accepts a discrete set of inputs (a story) along with a query, and outputs an answer.  
![Q&A](sukhbaatar2015end-to-end_2_a.png)  
#### Model Architecture
![Architecture](sukhbaatar2015end-to-end_2_b.png) 
* The inputs {x_i} and query q are transformed using input embedding matrices A and B, respectively. The embedded inputs are 'memories' in the embedding space. 
$$m_i = \text{Embed}_A(x_i)\qquad u = \text{Embed}_B(q)$$
* The most relevant embedded memory is matched with the embedded query by taking the inner product of each memory with the query followed by a softmax operation, thus producing a probability vector. The vector with the strongest score is used in subsequent steps. 
$$p_i = \text{softmax}(u^{\text{T}}m_i)$$  
* The unembedded inputs (story) are then embedded once again using an output embedding matrix C.  
$$c_i = \text{Embed}_C(x_i)$$  
* The response vector is then calculated by summing the inputs {c_i} and weighting each with the probability vector from the previous step.  
$$o = \sum_ip_ic_i$$  
* The final predicton, or answer to the question, is then calculated by summing the response vector with the initially embedded query, passing it through a weight matrix, and then applying a softmax operation.  
$$\hat{a} = \text{softmax}(W(o + u))$$  
* During training, utilizing stochastic gradient descent, the matrices A, B, C, and W are learned by minimizing the standard cross-entropy loss between the predicted label, and the correct label.  
## Variants 
* Along with the baseline model, the authors experimented with deepening the architecture by adding additional memory layers, which they term 'hops'.  
	* Each hop is comprised of embedding matrics A and C and outputs an answer, which is passed to the next layer as the query.    
* Two schemes are proposed for defining the input embedding A and output embedding B:  
$$\text{Adjacent: } A^{k+1} = C^k\qquad W^T=C^K\qquad B=A^1$$  
$$\text{Layer-wise: } A^1=A^2=...=A^k\qquad C^1=C^2=...=C^k$$ 
* Two sentence representations were explored: Bag of Words (BoW) which is agnostic to the position of words in a sentence, and a method they call Positional Encoding, which is sensitive to word position.  
* Given that some stories and questions depend upon the sequence of events which took place, a Temporal Encoding scheme is presented where the memory vectors {m_i} and the output vector are supplemented with a special matrix T which encodes temporal information.  
	* Random noise, in the form of empty memories, was injected into the temporal matrix to help with regularization during training.  
* Language modeling experiments were also performed where the model predicted the next word in a given sequence.
## Results  
![Results](sukhbaatar2015end-to-end_2_c.png)   

## TL;DR
* End-to-End Memory Networks utilize explicit memory and recurrent attention to achieve good performance on question answering and language modeling tasks.
* Compared to baseline Memory Networks, the End-to-End approach requires less supervision during training.
* While E2E networks do not outperform Strongly Supervised Memory Networks, experiments demonstrate they do outperform tuned RNNs and LSTMs of similar complexity.
