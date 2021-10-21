---
layout: summary
title: Summary
paper: {{zhou2019objects}}
# Please fill out info below
author: timchen0618
score: 10/10
---

TODO: Summarize the paper:
## What is the core idea?
Previous object detection methods identify objects as bounding boxes. However, it is not efficient as it is required to enumerate all possible bounding boxes; that is, the model need to consider object at all possible location and of all possible sizes. 

This paper detect the center point of each object using keypoint estimation, and then regress to the size of the bounding box.
The same framework also applies to tasks like 3D detection and human pose detection where they regress to other properties such as 3D size and pose.

## How is it realized (technically)?

### Keypoint Estimation
They try to produce a keypoint heatmap ..., where R is the output stride and C is number of keypoint types. (C=17 human joints in pose detection and C=80 object classes in object detection)
Ground truth heatmap is constructed using a Gaussian kernel, where each ground truth keypoint is the center of the Gaussian. 

The training objective is penalty-reduced pixel-wise logistic regression with focal loss:


To account for where the center point is in the RxR patch, they predict a offset for each of the center point. All classes share the same offset prediction. 

### Objection Detection
For each center point, the model also regresses to the size of the object . 
![image](https://user-images.githubusercontent.com/35536646/138213827-43be5b32-b964-49d8-ae57-b3b9235ddb8c.png)

So for each location, the model produce C+4 outputs at each location; C for the heat map, 2 for the offset and 2 for the size of the object.

![image](https://user-images.githubusercontent.com/35536646/138218692-51d6afb9-3f74-440c-aa5a-b818acda5f92.png)

### 3D Detection




* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
