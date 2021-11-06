---
layout: summary
title: Summary
paper: {{paper_tag}}
# Please fill out info below
author: # Your GitHub id
score: # How did you like this paper 0(dislike) to 10(love)
---
### What is the core idea? 

The introduces a two-fold approach to solving long-tail distribution problem in image recognitions by using representation learning and classification during the training process.

### How is it realized (technically)?

Long-tail distribution has been a common problem in real world recognition tasks because of imbalance in data classes.

[1] Learning representations

During training the authors used different sampling methods.Some of the methods are listed.

- Instance-balanced sampling

- Class-balanced sampling 

- Square-root sampling 

- Progressively-balanced sampling.


[2] Classifications 

The authors used this approaches to rebalance the classifier weights without any additional retraining.

- Classifier Re-training (cRT).

- Nearest Class Mean classifier (NCM)

- τ-normalized classifier (τ-normalized)

- Learnable weight scaling (LWS)

### How well does the paper perform?

#### Datesets 

Places-LT - 365 classes with  4980 to 5 images per class.

ImageNet-LT -  1000 classes with 1280 to 5 images per class.

iNaturalist - real-world data with consisting of samples from 8,142 species

#### Experimental Setup 

 Places-LT ,ResNet-152 as the backbone network and pretrain it on the full ImageNet- 2012 dataset, following Liu et al. (2019). 

 ImageNet-LT on ResNet- {10,50,101,152} and ResNeXt-{50,101,152}(32x4d) but mainly use ResNeXt-50 for analysis

 iNaturalist ResNet-{50,101,152}

SGD optimizer with momentum 0.9, batch size 512
cosine learning rate schedule from 0.2 - 0 on  224 × 224 image resolution. 

First representation learning stage, the backbone network is usually trained for 90 epochs. In the second stage, i.e., for retraining a classifier (cRT), we restart the learning rate and train it for 10 epochs while keeping the backbone network fixed.


![Sampling-1](kang2019decoupling_1a.png)

Comparison among different sampling methods

![Sampling-2](kang2019decoupling_1b.png)

ResNeXt-50 as backbone was fine-tuned with smaller (0.1×) learning rate on the last block and only retraining the linear classifier  

![Sampling-3](kang2019decoupling_1c.png)

Performance changes for the τ-normalized classifier varies and τ increases from 0 where many-shot accuracy decays dramatically while few-shot accuracy increases.


![Sampling-4](kang2019decoupling_1d.png)

Result using ImageNet-LT, comparison between backbones and SOTA methods .



![Sampling-5](kang2019decoupling_1e.png)


<!-- * What interesting variants are explored? -->

## TL;DR

* Long-tail problems can be solves using the right data sampling strategy

* Instance-balanced sampling  is a more generalizable  approaches  to learning representations.

