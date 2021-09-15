---
layout: summary
title: Summary
paper: {{salimans2016weight}}
# Please fill out info below
author: mmcinnestaylor 
score: # How did you like this paper 0(dislike) to 10(love)
---

TODO: Summarize the paper:
* What is the core idea?  
  * Salimans and Kingma propose weight normalization, a reparameterization of neural network weight vectors which they suggest leads to faster training via improving the conditioning of the optimization problem, and speeding up convergence of stochastic gradient descent.
* How is it realized (technically)?
  * The authors begin with standard neural network, where each neuron computes a weighted sum on input features followed by an elementwise nonlinearity. 
    * text w is a k-dimensional  weight vector, b a scalar bias term, x is a k-dimensional bias term, &phi;() a nonlinearity     
  y = &phi;(w &middot; x + b)  
  * 
    
  

* How well does the paper perform?  
  * Supervised Classification - CIFAR-10 using a modified ConvPool-CNN-C architecture
  * results image
  * Generative Modelling - MNIST \& CIFAR-10 using a deep Convolutional VAE
  * results image 
  * Generative Modelling - MNIST using DRAW
  * results image
  * Reinforcement Learning - Deep-Q-Network
  * results image
* What interesting variants are explored?   


## TL;DR
* Three
* Bullets
* To highlight the core concepts

