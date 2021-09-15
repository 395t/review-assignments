---
layout: summary
title: Summary
paper: ioffe2015batch
# Please fill out info below
author: ishanashah
score: 7
---

The core idea is to reduce internal covariate shift.

Internal covariate shift is the change in the distributions of network activations due to a change in netwrok parameters during training.

Internal covariate shift causes layers to continuously adapt to a new distribution (the layers are chasing a moving target).

Batch normalization reduces interval covariate shift via a normalization step that fixes the means and variances of layer inputs.



Normalization step goes between linear and non-linear layers.

Normalize the activations of a layer so they have 0 mean and unit variance.

Compute mean and standard deviation over all batches.

In the case of convolutional layers, compute mean and standard deviation over all batches and all spatial locations of a single channel.

Subtract mean and divide by standatd deviation for all activations.

During test time there are no batches, so use a running average mean and standard deviation from training time.



## TL;DR
* Three
* Bullets
* To highlight the core concepts
