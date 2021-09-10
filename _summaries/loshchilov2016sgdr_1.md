---
layout: summary
title: Summary
paper: loshchilov2016sgdr
# Please fill out info below
author: biofizzatreya
score: 6
---

TODO: Summarize the paper:
* What is the core idea?
  * The paper discusses a strategy for performing stochastic gradient descent with restarts (SGDR) for better convergence to a global minima. 
* How is it realized (technically)?
  * Normal stochastic gradient descent goes as: $$ x_{t+1} = x_t-\eta_t\cdot\nablaf_t(x_t) $$
  * Stochastic gradient descent with momentum goes as: $$ v_{t+1} = \mu_t\cdot v_t-\eta_t\cdot\nablaf_t(x_t) $$, and $$ x_{t+1} = x_t + v_{t+1} $$
  * In this situations $$ \eta_t $$ is the learning rate. In warm-restarts at $$ n $$ epochs, after each $$ n $$ epochs $$ \eta_t $$ is periodically reset to an initial value of $$ \eta_max $$ and then allowed to decay to $$ \eta_{min} $$ with a cosine annealing function. At the next restart the last solution $$ x_t $$ is taken as the initial condition. The annealing follows the given equation: $$ \eta_t = \eta^i_{min} + \frac{1}{2}\left( \eta^i_{max}-\eta^i_{min} \right)\left( 1+\text{cos}\left(\frac{T_{cur}}{T_i}\right)\rigth)$$
* How well does the paper perform?
  * The author's performed SGDR on CIFAR-10 and CIFAR-100 datasets. The test error of 4.03% on CIFAR-10 and 19.57% on CIFAR-100 can be improved to 3.51% on CIFAR-10 and 17.75% on CIFAR-100.
  * This points to the validity of this approach and also shows that this could be better than learning simply with momentum.
* What interesting variants are explored?
  * The authors also perform SGDR on EEG datasets.
  * The authors show that SGDR can achieve smaller test errors than the original learning rate schedule used.

## TL;DR
* Stochastic gradient descent with restarts
* Learning rate set at max value on restart and decays till next restart
* Performs as well as momentum based learning
