---
layout: summary
title: Summary
paper: smith2015cyclical
# Please fill out info below
author: liaojh1998
score: 7
---

_Note: LR stands for Learning Rate_

* What is the core idea?

    Increasing the learning rate might have short term negative effect but achieve a longer term beneficial effect.

    Dauphin et al. argument (saddle)

* How is it realized (technically)?

    The author tested multiple functional forms of cyclical LR windows (triangular, Welch (parabolic), Hann (sinusoidal)) and found that they all produced equivalent results. The triangular LR window was the simplest for implementation. Thus, the following triangular LR window was used:

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/2-Figure2-1.png" width="25%" height="25%">
    </p>

    The blue line represents the LR values changing between the `base_lr` and `max_lr`. Note that the `stepsize` is the number of iterations in half a cycle. Thus, for `stepsize` steps, LR will increase linearly from `base_lr` to `max_lr`, and then for another `stepsize` steps, LR will decrease linearly from `max_lr` to `base_lr`. This is done in code by adding the necessary amount of LR to the `base_lr` for each step, and use that value as the LR for the step.

    The author advocated the following guidelines:

    * **Good `stepsize`**: The number of **iterations in an epoch** is defined as the number of training images divided by the `batchsize`. So, if a dataset has 50,000 training images and the `batchsize = 100`, there are `50000/100 = 500` iterations in an epoch. According to experiments, it is often good to set `stepsize` equal to **2 to 10 times the number of iterations in an epoch**. Note that `stepsize` is half a cycle. 

    * **Good Stopping Point**: It is best to stop training at the end of a cycle because that's when LR is a minimum value and the accuracy peaks. However, it is up to the reader's discretion how many cycles to use. Experiments found that at least 3 cycles trained the network most of the way, but 4 or more cycles achieved even better performance.

    * **Reasonable Minimum and Maximum LR**: Do an "LR range test" by running the model for several epochs while increasing the LR from low to high values. Then, plot the accuracy vs. LR of the model like the following:

        <p align="center">
            <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/3-Figure3-1.png" width="25%" height="25%">
        </p>

        The maximum value for LR is when accuracy slows, becomes ragged, or starts to fall, like when `lr = 0.006` in this case. According to [Bengio 2012](https://arxiv.org/pdf/1206.5533.pdf), the optimum LR is usually within a factor of two of the largest LR that allows the model to converge. Thus, the minimum value for LR can be $$\frac{1}{3}$$ or $$\frac{1}{4}$$ of the maximum value.

* What interesting variants are explored?

    * `triangular2` and `exp_range`

* How well does the paper perform?

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/5-Table3-1.png" width="30%" height="30%">
    </p>

## TL;DR
* Three
* Bullets
* To highlight the core concepts
