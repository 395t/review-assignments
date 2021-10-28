---
layout: summary
title: Summary
paper: qi2017pointnet++
# Please fill out info below
author: ishank-arora
score: 9
---

## What is the core idea?

* PointNet was a pioneer in studying deep learning on point sets
  * However, by design, PointNet does not capture local structures which limits generalizability to complex scenes
* PointNet++ is a hierarchicahl neural network that applies PointNet recursively on a nested partitioning of the input point set. 
  * This network is able to learn local features

## How is it realized (technically)?

* Hierarchical strucuture<img src="qi2017pointnet++_1_a.png" alt="qi2017pointnet++_1_a" style="zoom:50%;" />
* PointNet uses a single max pooling operation, PointNet++ builds a hierarchichal grouping of points and progressively abstract larger and larger local regions along the hierarchy.
* Hierarchichal structutre has a number of *set abstrction* levels.
  * Here is where the set of points are processed and abstracted to produce a net set with fewer elements.
  * Done in three layers:
    * Sampling Layer
      * Selects a set of points from input points - defines centroids of local regions
    * Grouping Layer
      * Constructs local region sets by finding "neighboring" points around the centroids
    * PointNet Layer
      * Mini-PointNet to encode local region patterns into feature vectors
* Non-Uniform Sampling Density
  * PointNet++ intelligentally extracts multiple scales of local patterns and combines them at each abstraction level
  * Two types of density adaptive layers:
  * <img src="qi2017pointnet++_1_b.png" alt="qi2017pointnet++_1_b" style="zoom:50%;" />
  * Multi-scale grouping (MSG):
    * Simply conccatenate features at different scales to form a multi-scale feature
    * Train the network to learn an optimised strategty to combine the multi-scale features
  * Multi-resolution grouping (MRG):
    * MSG is computationally expensive
    * Avoids expensive computation while still presevering ability to adaptively aggregate information according to distributional properties of points

## How well does the paper perform?

* Experiments on 4 datasets - MNIST, ModelNet40, SHREC15, ScanNet
* <img src="qi2017pointnet++_1_c.png" alt="qi2017pointnet++_1_c" style="zoom:50%;" />

## TL;DR
* An extension of PointNet which allows for better learning of local features for better recognition of fine-grained patterns and generalizability 
* Learns by using increasing contextual scales
* Achieve state-of-the-art performance by using two novel set abstraction layers to intelligentaly aggregate multi-scale information
