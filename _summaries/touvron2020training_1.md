---
layout: summary
title: Summary
paper: touvron2020training_1
# Please fill out info below
author: specfazhou
score: 8/10
---

TODO: Summarize the paper:
* What is the core idea?  <br/>
Vision Transformer can achieved excellent results on image classification, but it requires large training datasets and computationally expensive. The authors of this paper came up with a data-efficient image transformer (DeiT) that use ImageNet as training datasets, which has same architecture as Vision Transformer, but by using different training methods and distillation, DeiT has better performance even than EfficientNet (see the following graph). In addition, DeiT is significantly less computationally expensive than Vision Transformer as well. 

<img width = 600 alt = "training_Deit_1" src = "training_Deit_1.png">

* How is it realized (technically)? <br/>
First, the distillation method requires one image classification model to be a teacher, and simply add one distillation token so that it can interact with class token and patch tokens in self-attention layers. As shown in the following graph <br/>
<image width = 300 alt = "training_Deit_2" src = "training_Deit_2.png">

There are actually two type of distillation methods -- soft distillation and hard distillation. The main difference between them is they use different objective functions.
  In general, denote $Z_s$ is logits of student model, $Z_t$ is logits of teacher model, $KL$ is Kullback-Leibler divergence loss, $L_{CE}$ is cross-entropy. $\phi$ is softmax function, and $y_{t} = argmax_{c} Z_{t} (c)$ <br/>
  **For soft distillation methods, the objective function is:** <br/>
  <img width = 600 alt = "training_Deit_3" src = "training_Deit_3.png"> <br/>
  **For hard distillation methods, the objective function is:** <br/>
  <img width = 600 alt = "training_Deit_4" src = "training_Deit_4.png"> <br/>
  
Second, during the training process, the authors use truncated normal distribution to initialize weights to avoid divergence. The authors also use several data-argumentation methods, and it seems all data augmentation methods help with performance.   
  
* How well does the paper perform?<br/>
  
  
  
* What interesting variants are explored?<br/>
  I don't think this paper mentions any variant of DeiT. 

## TL;DR
* Three
* Bullets
* To highlight the core concepts
  
