---
layout: summary
title: Summary
paper: reddi2019on
# Please fill out info below
author: aabayomi # Your GitHub id
score: 8/10 # How did you like this paper 0(dislike) to 10(love)
---

<!-- TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->

# Summary 1: ON THE CONVERGENCE OF ADAM AND BEYOND

## What is the core idea? ##

The problem is this paper is trying to solve is the limitation of optimizers such as ADAM in a convex setting. However the solution to this is to have history of past gradients.

### How is it realized (technically)? ###

First is to prove the non-convergence of ADAM.

<!-- $$
X_t_+_1 = X_t - \alpha_t m_t / 
$$ -->

<img width="700px" src="reddi2019on_1d.png"/>


<img width="700px" src="reddi2019on_1c.png"/>

Then modifying ADAGRAD

### How well does the paper perform? ###

<img width="700px" src="reddi2019on_1a.png"/>



### What interesting variants are explored? ###


<img width="700px" src="reddi2019on_1b.png"/>

AMSGRAD- smaller learning rates and better performance on synthetic datasets in relative comparison with ADAM

## TL;DR

* Keeping a gradient history improves performance
* Only exponential moving optimizers we used
