---
layout: summary
title: Summary
paper: radford2018improving
# Please fill out info below
author: chengchunhsu
score: 7/10
---


## What is the core idea?

Problem: **labeled data** for learning these speciﬁc tasks is limited

Solution: Introduced **Generative Pre-Training (GPT)** Model, a semi-supervised strategy for enhancing the performance on multiple NLP tasks.



## How is it realized (technically)?

Used architecture: Transformers

- Make longer-distance connections/dependencies in text
- Faster training



**Step #1: Unsupervised pre-training**

- Only use decoder of transformer

- Objective: maximize the likelihood

  ![1](radford2018improving_2_1.png)

- Predict context words

  ![2](radford2018improving_2_2.png)



**Step #2: Supervised fine-tuning**

- Use pre-trained model

- Add linear layer as the last layer

- Objective: maximize the likelihood

  ![3](radford2018improving_2_3.png)

- Auxiliary objective helps to improve the performance

  ![4](radford2018improving_2_4.png)



Some task requires special treatment:

- Textual entailment
- Similarity
- Question Answering and Commonsense Reasoning

![5](radford2018improving_2_5.png)



## How well does the paper perform?



- Benchmark
  - SOTA in 9 out of the 12 datasets



- Analysis
  - Impact of number of layers transferred
  - Zero-shot Behaviors
  - Ablation studies

![6](radford2018improving_2_6.png)

![7](radford2018improving_2_7.png)



## What interesting variants are explored?

- Language Models are Unsupervised Multitask Learners, NeurIPS'20

  



## TL;DR
* Apply one pre-trained model to many tasks
* Unsupervised pre-training decoder + supervised fine-tuning
* Language model served as an effective pre-training objective which could help model generalize well
