---
layout: summary
title: GELUs
paper: hendrycks2016gaussian
# Please fill out info below
author:  marcobueso
score:  10
---
## GELUs
* What is the core idea?\
The paper introduces the Gaussian Error Linear Units (GELUs) activation function for neural networks.\
The GELU function has provided performance improvement in practically all deep learning related fields.\
It could be said that the GELU still performs like a RELU in specific cases, such as when σ -> 0. The author discusses that the GELU can be considered a smooth RELU.\
For background, the RELU is simply the activation function where f(x) = max(0,x), basically zero-ing out any negative input.\
A main difference with the RELU however, is that rather than gating the inputs by their sign like the RELU does, the GELU gates the inputs based on their relative weight compared to other inputs.\

* How is it realized (technically)?\
The GELU is defined by the function 0.5x(1 + tanh[p2/π(x + 0.044715x3)]) \
Attempt at using math: $$ 0.5x (1+ tanh [ \sqrt{2/π} (x + 0.044715 x^3) ] )

* How well does the paper perform?\
The GELU activation function was tested on multiple classification tasks, such as the MNIST classification (handwritten digits dataset), tweet classification, TIMIT classification (speech recognition), CIFAR 10 and 100 (objects/image recognition, 10 and 100 classifications respectively) etc. 

* What interesting variants are explored?\
For simplicity, the GELU can also be modeled by xσ(1.702x). The author states that both approximations are easy to implement, and outperformed the other functions.

![image](https://user-images.githubusercontent.com/50091107/132141868-d439ff24-7198-459c-80ed-1644e5e1aa42.png)
*GELU activation function. Hansen, C. (22 Aug. 2019).*

## TL;DR
* GELU is an activation function similar to RELU. It is modeled by 0.5x(1 + tanh[p2/π(x + 0.044715x3)])
* It outperformed all other models across multiple classification tasks
* Although the paper is originally from 2016, it has getten more attention recently


