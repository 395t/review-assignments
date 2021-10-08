---
layout: summary
title: Summary
paper: jaegle2021perceiver
# Please fill out info below
author: ishank-arora
score: 9
---

* What is the core idea?
  * Perceiver is a model that builds upon Transformers
  * Scales to hundreds of thousands of inputs like ConvNets
  * Assymetric attention mechanism to **iteratively** distill inputs 
    * Allowing scale to handle very large inputs
  * Model is competitive or outperforms strong specialised models across various modalities
* How is it realized (technically)?
  * Architecture
    * Cross attention module - maps a byte array and a latent array to a latent array
    * Transformer tower that maps a latent array to a latent array
    * size of latent array is a hyperparameter
  * Position encodings
    * Permutation invariance and position information
    * Scalable Fourier Features
    * Position encodings are generally applicable.
* How well does the paper perform?
  * Pretty competitively with other models

## TL;DR
* Uses iterative attention
* Is a multimodal architecture
* Performs competitively against specialised models.
