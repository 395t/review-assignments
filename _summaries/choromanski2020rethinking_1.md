---
layout: summary
title: Summary
paper: choromanski2020rethinking
# Please fill out info below
author: joshpapermaster
score: 8
---

<!-- TODO: Summarize the paper:
* What is the core idea?
* How is it realized (technically)?
* How well does the paper perform?
* What interesting variants are explored? -->

While transformers have become a very popular way of working with sequential data, the equation to determine the attention of the model relies on softmax. This paper provides an alternative trick to approximate the attention in linear time complexity rather than the quadratic time complexity currently required. 

The authors suggest a new algorithm for performers called FAVOR+, which stands for fast attention via positive orthogonal random features. 

Using this approach brings the time complexity of attention from O(L^2 * D) to O(Lrd)
- This is beneficial because we can control r as a parameter and decrease the computational effort needed.

![favor+](choromanski2020rethinking_1b.png)

FAVOR+ uses a feature map to represent the kernel to keep time complexity low.

The similarities between the guassian kernel and the softmax kernel are noted, but guassian kernels can include negative values which leads to unstable results. 

The feature map allows for lower time complexity and the paper cites a recent publication of the gaussian kernel being represented by using a specific feature map. So this is expanded to include only positive results and stabilize the kernel. 

So they expanded on the guassian kernel to represent the softmax kernel as:

![favor+](choromanski2020rethinking_1c.png)

With h(x) in the feature map from the guassian kernel represented as:

![favor+](choromanski2020rethinking_1d.png)

So the original attention of:
![favor+](choromanski2020rethinking_1a.png)

is approximated by the more efficient version:
![favor+](choromanski2020rethinking_1e.png)

<!-- Include experiment information here -->

## TL;DR
- Performers provide a time and space efficient approximation of attention using the FAVOR+ approach
- They overcome the shortcomings of previous approximations that rely on priors or using localized data
- Performers work with transformers and can be extended to various uses