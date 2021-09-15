---
layout: summary
title: Summary
paper: ulyanov2016instance
# Please fill out info below
author: rll2396
score: 4
---

TODO: Summarize the paper:
* Core Idea

    Instance normalization can help a feed-forward generator network achieve better performance at stylizing images.

* Context
    * Gatys et al. (2016) showed promising results for using CNNs for the task of image stylization

    * The authors (2016) previously showed that the same task can be achieved hundreds of times faster at a cost to the quality of the images generated

    * In this paper they show that changing the normalization from batch to instance can improve the quality

* Implementation

    ![Stylization](ulyanov2016instance_1a.png)

    The generator network is a CNN that takes as input a random seed and a content image. The network is has a fixed style image to apply to the content image. The output is a stylized image.

    ![Contrast](ulyanov2016instance_1e.png)

    The end result is for the most part independent of the contrast of the content image. Thus, contrast normalization is needed. A simple way to implement this is 

    $$
    y_{tijk} = \frac{x_{tijk}}{\sum_{l=1}^W\sum_{m=1}^H x_{tilm}}
    $$

    where $$j$$ and $$k$$ are image dimensions, $$t$$ is the batch dimension, and $$i$$ is the channel dimension.

    This can be achieved through the usage of normalization layers.
    Batch Normalization is defined as 

    ![Contrast](ulyanov2016instance_1f.png)

    Instance Normalization is defined as

    ![Contrast](ulyanov2016instance_1g.png)

    The main difference is that Batch Normalization applies over a batch of images.

    ![Contrast](ulyanov2016instance_1b.png)

* Results

    The authors test this modification on both their previous network as well as a similar one from another paper.

    Here are the content and style images.

    ![Contrast](ulyanov2016instance_1c.png)

    Here are the stylized images. The top row is with batch normalization. The bottom row is with instance normalization.

    ![Contrast](ulyanov2016instance_1d.png)

## TL;DR
* Instance normalization is an alternative to batch normalization that can improve performance
