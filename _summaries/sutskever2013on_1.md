---
layout: summary
title: Summary
paper: sutskever2013on_1
# Please fill out info below
author: specfazhou
score: 9/10
---

TODO: Summarize the paper:
* What is the core idea? <br/>
The paper points that out classical momentum (CM) or Nesterov's accelerated gradient (NAG) can train DNNs and RNNs if initialization is well-designed and momentum coefficients are carefully chosen. It can achieve the performance only has been achieved by using Hessian-Free optimization (HF) before. Before this paper, people considered it was impossible to train DNNs and RNNs by using first-order method. 

* How is it realized (technically)? <br/>
First, the authors used CM and NAG to train deep autoencoders, which use sigmoid activication functions. They initialized parameters by using sparse initilization technique (SI), which makes each unit connect to 15 randomly chosen units in previous layer, and because input doesn't depend on the size of previous layer, they can't be easily saturated. the authors also chose momentum coefficient $$\mu_{t} = \min(1-2^{-1-log_{2}([t/250]+1)}, \mu_{max}$$ with $$\mu_{max} \in {0.999, 0.995, 0.99, 0.9, 0}$$   

* How well does the paper perform?

* What interesting variants are explored?


## TL;DR
* Three
* Bullets
* To highlight the core concepts
1. 
