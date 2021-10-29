---
layout: summary
title: Summary
paper: Zhao2020point
# Please fill out info below
author: # sritank
score: # 9/10

* Core idea?

They design a Point Transformer layer for point cloud processing suitable for point cloud labeling and segmentation. They introduce vector self-attention and trainable position encoding among others to make their residual transformer network invariant to permutation and cardinality. 

* Technical Implementation?

Given a set of feature vectors {x_i}, the vector self-attention function can be written as below:

![Vector attention](zhao2020point_2a.png)

where alpah(x) is the transformed features and gamma is the attention vector. They apply self attention locally with a neighbourhood of each datapoint in the cloud. The point transformer layer is created as follows:

![Point transformer layer](zhao2020point_2b.png)

They define their position encoding based on the point coordinates multiplied with trainable parameters as below:


![Position encoding](zhao2020point_2c.png)

The vector theta is an MLP which optimizes the encoding parameters. 

To reduce the cardinality of the point set, they introduce transition stages. At each transition stage they do a farthest point sampling to identify the subset of the desired cardinality. To do dense predicitions they introduce
a transition up step which maps the lower set to the higher order set using trilinear interpolation. The transition functions are illustrated below:

![Transition functions](zhao2020point_2d.png)

Finally they use a residual point transformer block which has a point transformer layer as shown below:

![REsidual point transformer](zhao2020point_2e.png)

Overall the network structure is as below:

![Network](zhao2020point_2f.png)


* Performance

They perform

* Interesting variants

## TL;DR
* Three
* Bullets
* To highlight the core concepts
