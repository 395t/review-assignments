---
layout: summary
title: Summary
paper: brock2021high-performance
# Please fill out info below
author: mattkelleher
score: 10
---

# Core Idea
The paper aims to create a class of Normalizer Free ResNets that are competative with the current state of the art.

An adaptive gradient clipping technique introdued can be used without any batch normalization and allows for smaller ResNet variants to be trained faster without a loss of accuracy and is used in their largest model which sets a new state-of-the-art top-1 accuracy on Imagenet. 
 
# Technical Details
Traditional gradient clipping methods are defined:

<img width="300px" src="brock2021high_performance_1_gradient_clipping.PNG"/>

The adaptive gradient clipping method introduced is defined below:

<img width="300px" src="brock2021high_performance_1_adaptive_gradient_clipping.PNG"/>

# Results

<img width="800px" src="brock2021high_performance_1_results.PNG"/>

# Normalizer Free Networks with Transfer Learning

<img width="400px" src="brock2021high_performance_1_tranfer_results.PNG"/>

## TL;DR
* Introduces an adaptive gradient clipping technique that is effective without any batch normalization present in network
* Decreased training time without losing accuracy in smaller models, set new top-1 state-of-the-art accuracy for ImageNet with large ResNet model 
* Out performed ResNet models with batch normalization on transfer learning tasks
