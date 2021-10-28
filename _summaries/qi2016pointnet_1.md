---
layout: summary
title: Summary
paper: qi2016pointnet
author: slycane9
score: 9
---
* What is the core idea?

Before this paper, state-of-the-art 3D classification/segmentation models all required 3D input to be transformed into voxel grids or multiple image views.  However, this paper introduces PointNets, which only requires point clouds as input to its model.  Using point clouds as input avoids issues with dense image inputs, and avoid irregularities that are difficult to learn from.

* How is it realized (technically)?

![arch](qi2016pointnet_1a.png)

Above is the architecture for PointNet.  The first layers go through an input and feature transformer.  These transformers are themselves mini networks and protect against variance in the point cloud input (ensuring we regard different transformations of the point cloud the same way).


Another part of the architecture is the split between a classification network and segmentation network.  This allows sharing of global knowledge with local knowledge.  As you can see in the above figure there is a connection between the two networks.

Finally, the MLPs and Max pooling layers are used to simulate a symmetric function.  A symmetric function is needed to protect against input permutations.  Looking at the symmetric function below, the MLPs represent collection h, and max pooling represents g.

![math](qi2016pointnet_1b.png)

* How well does the paper perform?

![classification](qi2016pointnet_1c.png)

Above we can see that PointNet outperforms other 3D input models, except for MVCNN which has a slight lead.

![segment](qi2016pointnet_1e.png)

In segmentation tests qualitatively seen above, PointNet also achieved State-of-the-art results.  Similar results were achieved in semantic scene segmentation tasks.

![flops](qi2016pointnet_1d.png)

Finally, PointNet achieved much higher classification speeds than other competitive models MVCNN and Subvolume.  The table above shows a 141 times decrease in FLOPS per sample compared to MVCNN.

## TL;DR
* PointNet uses only Point Clouds as input for 3D vision tasks
* Upholds input invariance with its architecture
* Outperforms most 3D models in classification/segmentation with great efficiency.