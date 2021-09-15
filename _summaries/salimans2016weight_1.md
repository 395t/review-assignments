---
layout: summary
title: Summary
paper: {{salimans2016weight}}
# Please fill out info below
author: mmcinnestaylor 
score: 7 # How did you like this paper 0(dislike) to 10(love)
---

## Core Idea  
 * Salimans and Kingma propose Weight Normalization, a reparameterization of neural network weight vectors which they suggest leads to faster training via improving the conditioning of the optimization problem, and speeding up convergence of stochastic gradient descent.  
 * This method is inspired by Batch Normalization, but unlike it, does not introduce dependencies amongst examples in a minibatch, thus (they claim) leading to better performance in applications such as recurrent models, deep reinforcement learning, and generative models where Batch Normalization is less successful. 
 * They also claim that while Weight Normalization is simpler to implement than Batch Normalization, it realizes nearly the same speed-up, while also being computationally less expensive.
## Technical Implementation
 * The authors begin with standard neural network, where each neuron computes a weighted sum on input features followed by an elementwise nonlinearity. 
   * text w is a k-dimensional  weight vector, b a scalar bias term, x is a k-dimensional bias term, &phi;() a nonlinearity     
 y = &phi;(w &middot; x + b)  
 * They then reparameterize the weight vectors, in terms of v, a k-dimensional vector, and g a scaling parameter  
   * Equation 2 here  
 * g may also be defined in terms of an exponential parameterization, where s is a log scale parameter learned by stochastic gradient descent  
   * Scale Equation here  
 * Training of the network used SGD, but the loss function now uses the reparameterizations above. Thus, the gradients in terms of those parameters are:  
   * Equation 3 here
   * Another formulation of the same gradients is:
   * Equation 4 here
   * This has the effect of scaling the weight gradient and projecting the gradient away from the current weight vector. The authors claim this brings the covariance matric of the gradient closer to the identity matrix, while also bebefiting optimization.
 * The authors also propose the following data dependent initlalization of the network parameters when using Weight Normalization. 
   * Equations 5, 6
   * The one downside to this initialization scheme is that it's application domains are limited to those where Batch Normalization performs well.      
    
  

## Performance  
#### Supervised Classification - CIFAR-10 using a modified ConvPool-CNN-C architecture
* results image
#### Generative Modelling - MNIST \& CIFAR-10 using a deep Convolutional VAE  
 * results image 
#### Generative Modelling - MNIST using DRAW  
 * results image
#### Reinforcement Learning - Deep-Q-Network  
 * results image
## Variants   
The authors propose a hybrid method which utilizes Weight Normalization and a special version of Batch Normalization, which they call Mean-Only Batch Normalization.
* Equations 7, 8
* This method leads to the centering of the gradients which are back propogated, and is computationally less expensive than full batch norm.  
* This method improves model accuracy at test time. 

## TL;DR
* Weight Normalization reparameterizes neural network weight vectors, leading to faster training via improved optimization conditioning and faster SGD.
* Weight Normalization is inspired by Batch Normalization, but is simpler to implement, computationally less expensive, and has broader applicability. 
* A hybrid method, Mean-Only Batch Normalization, uses both Weight Norm and Batch Norm, and outperforms both methods in classification on CIFAR-10.

