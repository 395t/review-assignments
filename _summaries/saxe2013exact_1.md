---
layout: summary
title: Summary
paper: saxe2013exact
# Please fill out info below
author: liyanc
score: 9
---

Summarize the paper:
* What is the core idea?

    The author proposed to analyze the dynamics of training deep networks by constraining on the linear network cases, which demonstrated similar behaviours to nonlinear ones.
The authors formulate the learning process as differential equations and developed analysis into the properties as a result of the dynamics, including symmetries, invariants, and stable points, which implies the network would reach optimal learning speed and convergence when initialized according to these properties.
Finally, the authors demonstrate the claims on MNIST and shed light on nonlinear case by arguing they share same properties due to the norm-preserving properties of the constructed network.
* How is it realized (technically)?

The author first stated with a three layer (two matrix multiplications) linear network case with quadratic loss.
Then the differential equations would be written as
$$
\tau \frac{d}{d t} W^{21}=W^{32^{T}}\left(\Sigma^{31}-W^{32} W^{21} \Sigma^{11}\right), \quad \tau \frac{d}{d t} W^{32}=\left(\Sigma^{31}-W^{32} W^{21} \Sigma^{11}\right) W^{21^{T}}
$$

Further, the author consider the case where input-output data are mean-substracted jointly gaussian variable with covariance matrices as statistics.
By assuming the input covariance is identity matrix, they derive the energy loss function as 
$$
E=\frac{1}{2 \tau} \sum_{\alpha}\left(s_{\alpha}-a^{\alpha} \cdot b^{\alpha}\right)^{2}+\frac{1}{2 \tau} \sum_{\alpha \neq \beta}\left(a^{\alpha} \cdot b^{\beta}\right)^{2}
$$
In this equation, we see that the first term implies the vectors in weight matrices should be colinear to minimize the loss, while the second term requires othorgonality.
Therefore, the result is a set of vectors that are either pairwise orthogonal or colinear.
The authors further examine the invariance manifold of weight vectors and find that their modes in the spectra evolve independently and staying orthogonal.
With similar but limited noisy initial condition, the authors find that the learning speed follows a sigmoid function as described in
$$
u_{f}(t)=\frac{s e^{2 s t / \tau}}{e^{2 s t / \tau}-1+s / u_{0}}
$$
, which coincides with the experiment well.

  Then the authors generalize to a multi-layer linear network case assuming all weights are orthogonal.
The differential equation can be therefore written as $$\tau \frac{d}{d t} u=N_{l} u^{2}(s-u)$$, which imples that the learning speed converges to constant when the number of layers goes to infinity.
* How well does the paper perform?
  The author proposed a pretraining scheme accordingly by first auto-encoding the input data and switching to the actual training.
  On the MNIST dataset, the loss function demonstrates a step-function-like drop while the randomly-initialized one demonstrates a sigmoid-like drop.
* What interesting variants are explored?
  The author moves toward nonlinear deep networks and claims that the properly-initialized networks have the norm-preserving property and therefore plays nicely with nonlinear functions without deminishing or saturating.
They perform experiments to validate the claim as well.

## TL;DR
* Solving linear networks analytically as diffeqs demonstrates properties (symmetries, invariants) which have implications on the learning dynamics of them.
* With such invariants, there is a manifold where the learning trajectory is optimal
* Initializing the weights on the manifold gives rise to fast and converging learning dynamics, which is validated by experiments

