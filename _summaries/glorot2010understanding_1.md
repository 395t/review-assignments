---
layout: summary
title: Summary
paper: glorot2010understanding
# Please fill out info below
author: slycane9
score: 7
---

Methods of training deep neural networks at the time (through back-propogation and random initialization) were not successful.  This is because the attempts at training in these methods would often result in training weights plateauing.


This paper explores alternative methods that can be used to better train these deep multi-layer networks.  Two of the main methods are  normalized initialization and the softsign activation function.


The researchers used a synethetic image dataset called Shapeset-3 x 2 to test their training configurations.  The network consisted of five hidden layers of size 1000 with a softmax on the model's output layer.

The paper's main contribution is a new initialization method called Normalized Initialization, which normalizes the initialization values of a layer based on its depth in the network.

Normalized Initialization is used on the weights in the following way:

$$
W \sim U [-\frac{\sqrt{6}}{\sqrt{n_j + n_{j+1}}}, \frac{\sqrt{6}}{\sqrt{n_j + n_{j+1}}}]
$$

This method avoids having the weights gradients in each layer of the network vary by different amounts (ie avoids the bottom layer having a much higher variance than the top layer).  The results show lower error rates with Normalized Initialization compared to Standard Initialization.

The paper also tested the activation function in the model's hidden layers.  

* Sigmoid
	* Caused early saturation of top layer (impedes learning)
	* This saturation is likely because an output of 0 created by random initialization causes saturation in the sigmoid function.
	* Yielded the highest test error when compared to the other activation functions
* Hyperbolic Tangent
	* Causes layers to saturate one after the other (from first to last)
	* Causes higher error rates than Softsign
	* Gains the most improvement from using Normalized Initialization over Standard Initialization
* Softsign
	* Similar to Hyperbolic Tangent except it has polynomial asymptotes (causing a smoother curve)
	* Its activation values follow the same trend at every layer and end at larger values
	* Achieves the lowest error rate compared to the other two functions.


The logistic regression cost function was chosen over the quadratic cost function because of earlier findings (Solla et al., 1988) and an experiment that showed the training criterion for the quadratic cost function was too low and flat compared to logistic regression.


This paper does a good job of exploring the possibilties of new training configurations with detailed experimentation and analysis.

## TL;DR
* Solving training issues of deep networks
* Analyzed variance of activations and gradients by layer
* Good results from Softsign and Normalized Initialization
