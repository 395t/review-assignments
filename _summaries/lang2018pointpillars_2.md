---
layout: summary
title: Summary
paper: lang2018pointpillars
# Please fill out info below
author: aabayomi
score: # How did you like this paper 0(dislike) to 10(love)
---
<!-- 
TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->

# Core Idea

The authors proposes as much faster approach by which encoder that learns point cloud representations by stacking learned features as vertical tensors. 

# Main Contributions

![](lang2018pointpillars_2a.png)

* Representation of the 3-D lidar point cloud inputs as pseudo-images

* 2-D convolutional backbone processes the images

* Single-shot detectors regresses to 3D boxes

# Loss function 

The loss formulation combines the sotfmax classification loss, focal loss on object classification  and localization loss.This is optimized using Adam of learning rate of $2 * 10^−4$ with a decay rate 0.8 at every 15 epoch.

![](lang2018pointpillars_2b.png)


# Performance

On KITTI datasets PointPillars  outperforms fusion based methods on cars and cyclists my respect to mean average precision (mAP) compared to lidar-only methods.

![](lang2018pointpillars_2c.png)

PointPillar is faster compared to SOTA on BEV

![](lang2018pointpillars_2d.png)

## TL;DR

* PointPillars encoder is computationally efficient and performant on object detection. 

* Data Augmentation is required for good performance