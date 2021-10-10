---
layout: summary
title: Summary
paper: graham2021levitt
# Please fill out info below
author: biofizzatreya
score: 8
---

The paper attempts to combine, convolutional networks and training principle from CNNs with vision transformers. While transformers can generalize well over large datasets, transformers themselves have certain problems. Transformers lose all positional information and since most images are locally similar, it takes more data to train vision transformers. Moreover due to quadratic complexity of the self-attention matrix, transformers have difficulty dealing with large images. LeVit's solution to these problems is instead of feeding an image to the transformer, they feed a image after passing it through multiple convolution layers.

![image](https://user-images.githubusercontent.com/13065170/136635751-c21a6e5d-c6ce-4813-bda9-4f3ef884e265.png)
![image](https://user-images.githubusercontent.com/13065170/136635765-4209a6b7-7e90-436c-a96f-2cb958586416.png)

LeVit design principles:
* Small convnet applied to input of Transformers
* Two output heads
* Hardswish activations
* Batch-norm after every convolution
* Attention shrinking layers

![image](https://user-images.githubusercontent.com/13065170/136635772-1c66741e-e1f9-4927-af8c-df03e3d3ad3b.png)
![image](https://user-images.githubusercontent.com/13065170/136635778-6ab9bdbe-7889-4779-b60a-204815006999.png)

LeVit is trained by a teacher network. One head performs classification with cross-entropy loss the second from a  RegNetY-16GF trained on imageNet.
![image](https://user-images.githubusercontent.com/13065170/136635784-094d7434-e487-40a4-b3fa-a14a7eb44a4e.png)

Ablations:
To understand LeVit's performance they performed multiple ablation studies by selectively changing different parts of the network:
* Lack of pyramidal attention - loss of accuracy
* Without patchConv - loss of accuracy
* Without batchnorm - slows down training
* Removing teacher model - slows down training
* Removal of hardswish non-linearity - degrades performance

## TL;DR
* Convolutional operations applied to transformer stacks
* Self-attention shrunk for speed and accuracy
* Results in much faster object classification 
