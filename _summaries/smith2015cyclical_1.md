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

    This paper proposes a learning rate policy where the learning rate oscillates between two bounds and a method to estimate the two bounds reasonably.

    According to [Dauphin et al., 2015](https://arxiv.org/pdf/1502.04390.pdf), loss is more difficult to minimize due to saddle points rather than poor local minima, and increasing the learning rate allows for more rapid traversal away from saddle points. Also, increasing the learning rate might have short term negative effects but can achieve beneficial effects in the long term. The author showed this when training GoogleNet on ImageNet:

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/8-Figure12-1.png" width="25%" height="25%">
    </p>

    Although the validation accuracy decreased during periods of increasing LR, the accuracy improved with higher gains during periods of decreasing LR. Thus, cyclical LR policy may speed up training to achieve better accuracy in the long run. It also removes the need to guess the optimal LR to use at each timestep in training.

* How is it realized (technically)?

    The author tested multiple functional forms of cyclical LR windows (triangular, Welch (parabolic), Hann (sinusoidal)) and found that they all produced equivalent results. The triangular LR window was the simplest for implementation. Thus, the following triangular LR window was used:

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/2-Figure2-1.png" width="20%" height="20%">
    </p>

    The blue line represents the LR values changing between the `base_lr` and `max_lr`. Note that the `stepsize` is the number of iterations in half a cycle. Thus, for `stepsize` steps, LR will increase linearly from `base_lr` to `max_lr`, and then for another `stepsize` steps, LR will decrease linearly from `max_lr` to `base_lr`. This is done in code by adding the necessary amount of LR to the `base_lr` for each step, and use that value as the LR for the step.

    The author advocated the following guidelines:

    * **Good `stepsize`**: The number of **iterations in an epoch** is defined as the number of training images divided by the `batchsize`. So, if a dataset has 50,000 training images and the `batchsize = 100`, there are `50000/100 = 500` iterations in an epoch. According to experiments, it is often good to set `stepsize` equal to **2 to 10 times the number of iterations in an epoch**. Note that `stepsize` is half a cycle. 

    * **Good Stopping Point**: It is best to stop training at the end of a cycle because that's when LR is a minimum value and the accuracy peaks. However, it is up to the reader's discretion how many cycles to use. Experiments found that at least 3 cycles trained the network most of the way, but 4 or more cycles achieved even better performance.

    * **Reasonable Minimum and Maximum LR**: Do an "LR range test" by running the model for several epochs while increasing the LR from low to high values. Then, plot the accuracy vs. LR of the model like the following:

        <p align="center">
            <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/3-Figure3-1.png" width="20%" height="20%">
        </p>

        The maximum value for LR is when accuracy slows, becomes ragged, or starts to fall, like when `lr = 0.006` in this case. According to [Bengio 2012](https://arxiv.org/pdf/1206.5533.pdf), the optimum LR is usually within a factor of two of the largest LR that allows the model to converge. Thus, the minimum value for LR can be $$\frac{1}{3}$$ or $$\frac{1}{4}$$ of the maximum value.

* What interesting variants are explored?

    The author proposed two variations of cyclical LR:

    * `triangular2`: This is same as the `triangular` policy, but the learning rate difference is cut in half at the end of each cycle like the following:

        <p align="center">
            <img src="https://pyimagesearch.com/wp-content/uploads/2019/07/keras_clr_triangular2.png" width="30%" height="30%">
        </p>

    * `exp_range`: Similar to the `triangular` policy, but the `max_lr` decreases by an exponential factor of $$\gamma^{\text{iteration}}$$ like the following:

        <p align="center">
            <img src="https://pyimagesearch.com/wp-content/uploads/2019/07/keras_clr_exp_range.png" width="30%" height="30%">
        </p>

    Note that different cyclical LR schedules with different boundary values can be appended one after the other. The author did this on the CIFAR-10 baseline by training it with sequential `triangular2` policies with the following boundary values:

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/4-Table2-1.png" width="25%" height="25%">
    </p>

* How well does the paper perform?

    The author tested the LR schedule on multiple models designed for image classification. They used the CIFAR-10, CIFAR-100, and ImageNet datasets. Generally, the models performed the best when trained with cyclical LR or its variants, averaging about a 0.8% increase in accuracy over a fixed LR schedule. Here's a summary of comparisons: 

    <p align="center">
        <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/4-Table1-1.png" width="25%" height="25%">
    </p>

    For clarifications, `decay` is a LR policy with boundary values in where LR starts at `max_lr` and is reduced to `base_lr` after some iterations, then the LR is kept at `base_lr` for all iterations after. `exp` is an exponential decay policy for LR.

    The author notes the following in general:

    * `triangular2` policy usually trained the model in less iterations for comparable accuracy. Training longer on `triangular2` outperforms training on a `fixed` LR policy.
    * Adaptive learning rate methods can combine with cyclical LR to obtain comparable accuracy as shown in the following:

        <p align="center">
            <img src="https://d3i71xaburhd42.cloudfront.net/37b5dfe87d82ba8f310155165d5bf841dc92dea2/5-Table3-1.png" width="25%" height="25%">
        </p>

        Note that some methods (AdaGrad, AdaDelta) when combined with CLR, while using only 25k iterations of training, still gained a final accuracy that is equivalent to the final accuracy of the method without CLR, which used 70k iterations of training. Refer to the next lecture for explanations on these methods.

    * Training ResNet, Stochastic Depth networks, and DenseNets with cyclical LR performed better than training with a fixed LR by about 0.2% increase in accuracy on average for CIFAR-10 and by about 0.5% increase in accuracy on average for CIFAR-100.

## TL;DR
* CLR oscillates the learning rate between a minimum and maximum value during training.
* CLR removes the need to tune an optimal schedule for LR.
* CLR can train the network faster to achieve a better accuracy in the long run.
