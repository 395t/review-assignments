---
layout: summary
title: Summary
paper: he2015deep
author: philkr
score: 10
---

If AlexNet started the modern era of deep learning, ResNets made sure it would spread to all of computer vision and beyond.
The core idea of residual networks is to parametrize each layer (or group of layers) as a residual of a function.
A function $$f_1(x)$$ would now become $$f_2(x) = x + g(x)$$.

<img width="200px" src="he2015deep_1a.jpg"/>

Both representations have the same expressional power and computational requirements.
However, they have a different gradient.
For regular networks, back-propagation multiplies a gradient with $$\frac{\partial}{\partial x} f_1(x)$$, while residual networks use $$\frac{\partial}{\partial x} x + g(x) = I + \frac{\partial}{\partial x} g(x)$$.
Hence, back-propagation passes the gradient back directly, and adds a second component multiplied by $$\frac{\partial}{\partial x} g(x)$$.

Fun fact, the backward pass of a resnet block looks the same as the forward pass 

<img width="200px" src="he2015deep_1b.jpg"/>

How do we build a network out of this idea?
There are two variants of basic-residual network blocks: post-activation blocks (below left), pre-activation blocks (below right).

<img width="200px" src="he2015deep_1c.jpg"/>

ResNets then stack many of these blocks in a network

<img width="100px" src="he2015deep_1d.jpg"/>

The first layer if each series of blocks is strided, and it's residual connection uses a 1x1 convolution (to better deal with the change in number of channels).

ResNets really blew the competition out of the water across many computer vision tasks. 
They are still used today.

## TL;DR
* Introduces **ResNet**: First really deep networks
* Beautiful **mathematical interpretation**
* **Stellar results**

