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


TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
