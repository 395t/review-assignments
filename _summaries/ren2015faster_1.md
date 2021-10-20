---
layout: summary
title: Faster R-CNN Towards Real-Time Object Detection with Region Proposal Networks
paper: ren2015faster
# Please fill out info below
author: saikm200022
score: 8
---

# **Summary - Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks**

## What is the core idea?

Despite state of the art results achieved by region-based CNNs such as Fast R-CNN, there is a computional bottleneck during test time when finding region proposals. This paper suggests a deep learning approach for determining region proposals called Region Proposal Networks that leads to more efficient object detection for Fast R-CNN architecture. These RPNs addresses the issue of the bottleneck because convolutional feature maps are now shared between the RPN and the object detection classifer network. On top of the efficiency of object detection, the paper suggests a new concept called anchor boxes that allows the RPN to consider bounding boxes at various scales and aspect ratios.

![Alt Text](ren2015faster_2_1a.PNG)

## How is it realized (technically)?

Region Proposal Networks (RPN) take an image as input and produce object proposal rectangles that each have some score. In this paper, the RPN used was simply a Fully Convolutional Network. During the convolution, each 3 x 3 window is mapped to a feature at a lower dimension and is then fed to two separate fully connected layers. The first is a box regression layer, which computes the coordinates of the bounding boxes. The second is a classification layer which outputs an estimated value for the probability of that specific box being an object or not. 

The paper talks about the concept of anchors which is the center of the 3 x 3 sliding window considered during convolution. Using this anchor, they come up with different anchor boxes (total of 9 for 3 x 3 window) for different scales and aspect ratios. 

![Alt Text](ren2015faster_2_1b.PNG)

An important feature of this paper is the ability to share convolution feature maps between the RPN and the Fast R-CNN object detection network. They use a 4 step training algorithm to achieve this:
1. Train the RPN using stochastic gradient descent and backpropogation. Using a pre-trained Imagenet model initialization that is fine-tuned
1. Train the detection network from Fast R-CNN using proposals from previous step
1. Initialize RPN with Detection Network parameters and keep the shared convolutional layers constant
1. Fine tune layers in the RPN and Fast R-CNN that are unique to themselves


TODO: Summarize the paper:
* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
