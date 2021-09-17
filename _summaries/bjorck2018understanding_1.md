---
layout: summary
title: Summary
paper: {{bjorck2018understanding}}
# Please fill out info below
author: # timchen0618
score: # How did you like this paper 0(dislike) to 10(love)
---

TODO: Summarize the paper:
## Background
Normalizing the input data to zero-mean and constant standard deviation has long been recognized as good practice in training neural networks. Batch normalization extend this idea to the input of each layer and achieve immense success in various datasets. However, little is known about the reason for the improvement. 

## Core idea 
The paper pointed out that batch normalization (BN) is beneficial to training neural networks mainly because it allow for larger learning rates. The author showed that by limiting the input to zero-mean and unit standard deviation, larger step size can be used. It also proved that larger learning rates in networks without BN could lead to divergent loss and undesirable behaviors of gradients and activations. 

* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
