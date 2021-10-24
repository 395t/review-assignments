---
layout: summary
title: Summary
paper: zhu2020deformable
# Please fill out info below
author: mattkelleher
score: 8 # TODO
---

## Core Idea
Extends DETR by focusing the attention modules onto a small set of sampling points by using the idea of deformable convolution. 
This allowing for better results in significantly fewer training epochs and addresses the issues DETR has when attempting to detect small objects. 


## Technical Implementation
Below we see the a representation of the Deformable DETR model.
We see that convolutional features maps are extracted from an image using a convolutional neural network (the authors used ResNet-20) before being fed into the encoder attention module.
Information from the encoder along with object queries are then fed into the decoder to produce bounding boxes.

<img src="zhu2020deformable_2_model.PNG" width="850" />

Revisitng issues with DETR:
- Requires significantly more training epochs than other object detectors
  - **Why?**  Right after initalization the cross attention modules look at all features and slowly learn which features are most important ultimately leading to sparse attention map.
  - Adding the deformable attention acts as a catalyst to identifying the sparse attention map and as a result the network is able to more directly and quickly learn which features to focus in on.
- Struggles with small objects
  - **Why?** In other object detectors higher resolution feature maps are used. Due to the nature of self attention the size of the feature map is realted quadratically to the self attention complexity which forces lower resolution feature maps to be used to achieve reasonable complexity.
  - In the Deformable DETR the deformable self attention allows for attention to focus on key elements ultimately boosting the performance on smaller objects.


Seen below is the deformable attention module introduced in this paper. 


<img src="zhu2020deformable_2_attention.PNG" width="900" />

It is very similar to a normal attention module with the addition of the learned Sampling Offsets block seen above. 
We can also see from the equations below that the deformable attention is only a slight modification of the general multi head attention. 

<img src="zhu2020deformable_2_MultiheadAttn.PNG" width="700" />

<img src="zhu2020deformable_2_DeformAttn.PNG" width="700" />

## Results

<img src="zhu2020deformable_2_results.PNG" width="900" />

## Two-Stage Deformable DETR


## TL;DR
* Combines the ideas of DETR and deformable convolution to create end to end object detection model 
* Outperforms DETR and can be be trained in significantly fewer epochs
* Explores a Two-Stage deformable DETR model which further boosts performance 
