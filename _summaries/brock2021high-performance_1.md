---
layout: summary
title: Summary
paper: brock2021high-performance
# Please fill out info below
author: mattkelleher
score: 9
---

# Core Idea
The paper aims to create a class of Normalizer Free (NF) ResNets that are competative with the current state-of-the-art.
An Adaptive Gradient Clipping (AGC) method is introduced to achieve these goals with NF ResNets.  

# Motivation
While batch normalization has been shown to be effective in practice, it is difficult to explain why it works and has some practical drawbacks.

The authors outline three of these drawbakcs which are summarized below: 
1. Batch Normalization is computationally expensive: requires signifcant memory overhead and can be slow due to gradient evaluations.
2. Models behave differently during training and testing.
3. Batch normalization violates the assumption that training examples are indepenent of each other within the same minibatch.

The goal of this paper is to address these issues and create normalizer free ResNets with comperable accuracies as the current state-of-the-art, many of which use normalization.

 
# Technical Details
Traditional gradient clipping methods are defined:

<img width="300px" src="brock2021high_performance_1_gradient_clipping.PNG"/>

Adaptive Gradient Clipping (AGC):

<img width="300px" src="brock2021high_performance_1_adaptive_gradient_clipping.PNG"/>

# Results

<img width="800px" src="brock2021high_performance_1_results.PNG"/>

# Normalizer Free Networks with Transfer Learning

<img width="400px" src="brock2021high_performance_1_transfer_results.PNG"/>

## TL;DR
* Introduces an adaptive gradient clipping technique that is effective without any batch normalization present in network
* Decreased training time without losing accuracy in smaller models, set new top-1 state-of-the-art accuracy for ImageNet with large ResNet model 
* Out performed ResNet models with batch normalization on transfer learning tasks
