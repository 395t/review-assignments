---
layout: summary
title: Summary
paper: cai2017cascade
# Please fill out info below
author: DartingMelody
score: 9
---

**What is the core idea?**

The central idea of the paper is to train multiple detection heads with multiple intersection over union (IoU) thresholds. The cascade R-CNN architecture solves two problems, overfitting during training and inference-time mismatch between the IoU for which the detector is optimal versus IoU of the input hypothesis. The model consists of sequence of detectors trained with increasing IoU thresholds with the ouptut of the previous detector is fed into the next as a resampling mechanism with no discrepancy between training and inference.

![Problem example](./cai2017cascade_1a.png)

**How is it realized (technically)?**

![Architecture](./cai2017cascade_1b.png)

* Cascade-RCNN extends the two-stage architecture of faster-RCNN relying on a cascade of specialized regressors where _T_ is the total number of cascade stages. Each regressor ft in the cascade is optimized with respect to the sample distribution {bt} arriving at the tth stage, instead of initial distribution b1. 

![Regressor equation](./cai2017cascade_1c.png)

* At each stage t, the RCNN has a classifier ht and regressor ft which is optimized for IoU threshold ut

![Detector loss equation](./cai2017cascade_1d.png)

where ut > u(t-1). This is achieved by minimizing the loss where bt is  ft−1(x , b ), g is the ground truth object for xt, λ = 1 the trade-off coefficient,  yt is the label of xt given by

![Output equation](./cai2017cascade_1e.png)

* Cascade R-CNN have four stages, one RPN and three for detection with U = {0.5, 0.6, 0.7}

**How well does the paper perform?**

The Cascade R-CNN, based on FPN+ and ResNet-101 outperforms all the earlier state of the art single model detectors like Faster-RCNN, YOLO, Mask-RCNN etc on COCO dataset. It also outperforms Iterative BBox and Integral Loss. The difference in result is more visible with higher IoU. As the computational cost of detection head is usually small, when compared to RPN, the computational overhead of RCNN is small for both training and testing. 

![Results](./cai2017cascade_1f.png)

**What interesting variants are explored?**

Various architectures like Faster-RCNN, R-FCN with ResNet-50 and ResNet-101 backbone, FPN+ with ResNet-50 and ResNet-101 backbone are trained with and without cascading. The cascade variants of all these models outperforms the corresponding non-cascade models. Other ablation experiments were performed on IoU threshold, stagewise comparison and number of stages with the result that the three stage cascade (the cascade-RCNN model ) achieves the best tradeoff. 


## TL;DR
* The cascade-RCNN model consists of sequence of detectors trained with increasing IoU thresholds. 
* The model aims to reduce overfitting, matchc inference and training architecture, and detect true positives while supressing close false positives,
* The Cascade-RCNN model outperforms all the previous models like Fast RCNN, YOLO, Mask-RCNN, etc on COCO dataset. 
