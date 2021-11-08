---
layout: summary
title: Summary
paper: zhang2020contrastive
# Please fill out info below
author: biofizzatreya
score: 5
---

TODO: Summarize the paper:
* What is the core idea?
The paper attempts to bridge the lack of labelled datasets in medical images by training a pair of neural networks on image and corresponding text data. The purpose of the network is to reconstruct correct text labels given a medical image and vice-versa in an unsupervised fashion. 
* How is it realized (technically)?
![image](https://user-images.githubusercontent.com/13065170/140814023-53873e6b-2651-4268-aca1-ea83862696e3.png)
A set of paired inputs is denoted by $$ (x_v, x_u) $$ where $$ x_v $$ is an image and $$ x_u $$ is a piece of text. Both inputs are passed through random transformations and then through an encoder. For images, the encoder is a ResNet-50 and for texts it is BERT. The encoder vector is further transformed with a single layer network. Following this, two losses are computed to ensure the true pairs always have minimum loss values in spite of the noise from random transformations.
image to text loss:
![image](https://user-images.githubusercontent.com/13065170/140814113-12a4a937-e7f7-4a33-87bb-6f116783ed3e.png)
text to image loss:
![image](https://user-images.githubusercontent.com/13065170/140814152-d27ce6eb-8c06-4cb1-9bcb-222307a9f844.png)
final loss:
![image](https://user-images.githubusercontent.com/13065170/140814186-7c20d1b3-f8ad-40c2-a5a3-ac0c922ae121.png)

* How well does the paper perform?
The paper beats previous benchmarks. However the agreement of these results strongly rely on the nature of transformations.
![image](https://user-images.githubusercontent.com/13065170/140814243-e43e1110-d079-427a-b644-2f383edb4a29.png)
![image](https://user-images.githubusercontent.com/13065170/140814271-04183930-7f07-4bd7-a313-4ff56570d376.png)

* What interesting variants are explored?
ConVirt performs better for zero-shot image retrieval tasks.
![image](https://user-images.githubusercontent.com/13065170/140814451-3007112e-8ca2-4c72-bcd9-b02479d32ed7.png)

The paper explores some of the hyperparameters involved in the training. One of the examples show that the loss function parameters strongly influence learning.
![image](https://user-images.githubusercontent.com/13065170/140814495-51963f98-3bfb-4558-ba3e-ec5c0c1f3a10.png)

## TL;DR
* Unsupervised text-image matching
* Developed for medical images
* Relies strongly on loss hyperparameters
