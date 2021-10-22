---
layout: summary
title: Summary
paper: carion2020end-to-end
# Please fill out info below
author: chengchunhsu
score: 7
---



## What is the core idea?

<u>Core idea</u>: transform object detection problem as a direct set prediction problem



<u>Motivation</u>: avoid hand-designed components in modern object detectors

- E.g., NMS and anchor generation



<u>Solution</u>: DEtection TRansformer (DETR)

- a set-based global loss that forces unique predictions via bipartite matching
- a transformer encoder-decoder architecture



## How is it realized (technically)?

![image-20211022151426913](.\carion2020end-to-end_2_1.png)

Key component:

- a set prediction loss that forces unique matching between predicted and ground truth boxes
- an architecture that predicts (in a single pass) a set of objects and models their relation



**<u>Set prediction loss</u>**

DETR infers a ﬁxed-size set of N predictions

<u>Goal</u>: score predicted objects (class, position, size) with respect to the ground truth

<u>How</u>:

- Our loss produces an optimal bipartite matching between predicted and ground truth objects
- After that, we optimize object-speciﬁc (bounding box) losses



Match loss:

![image-20211022151454271](.\carion2020end-to-end_2_2.png)

Hungarian loss:

![image-20211022151507583](.\carion2020end-to-end_2_3.png)

Bounding box prediction loss:

![image-20211022151533727](.\carion2020end-to-end_2_4.png)



**<u>Transformer architecture</u>**

![image-20211022151602124](.\carion2020end-to-end_2_5.png)

- CNN backbone
  - Generate a low-resolution feature map with 32x downsampling and 2048 channels
- Encoder-decoder transformer
  - Encoder input: a flatten feature map with + positional encoding
  - Decoder output: object queries
- Feed forward network (FFN)
  - *Independently* decode the object queries into box coordinates and class labels



## How well does the paper perform?

<u>Performance on COCO</u>

![image-20211022151621018](.\carion2020end-to-end_2_6.png)



<u>Ablation studies</u>

![image-20211022151701535](.\carion2020end-to-end_2_7.png)



<u>Generalization to unseen numbers of instances</u>

![image-20211022151713958](.\carion2020end-to-end_2_8.png)



## TL;DR
* Transform object detection as a direct set prediction problem
* Propose a set-based global loss that forces unique predictions via bipartite matching
* Demonstrate DETR achieves accuracy and run-time performance on par with existed method
