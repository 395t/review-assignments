---
layout: summary
title: Summary
paper: bottou2010large
author: elampietti
score: 8
---

Datasets have grown to a point where machine learning is now constrained by computing time rather than a need for more training data.
Bottou proposes that stochastic gradient descent is an effective machine learning algorithm for this excess of data.
Since large scale datasets are not limited by the amount of data available, the optimization error can be increased to allow the computing reasources to be used more effectively.

Stochastic gradient descent randomly chooses a datapoint to calculate the gradients at each iteration rather than calculating each datapoint to reduce the computational cost.

![SGD](https://user-images.githubusercontent.com/7085644/132602146-a90027db-61db-4ad7-8a6f-1d2f72966bcc.PNG)

Empirical risk: En(f) -> training set performance

Expected risk: E(f) -> generalization performance on future examples

The function, f*, represents a the best prediction function that we can obtain given our start to stochastic gradient descent.
Therefore, we let F encompass the family of functions acquired during SGD from the chosen parameters where f* is the function that minimizes E(f).
Finding the expected risk E(f) can be costly, therefore the empirical function is optimized to a specific accuracy. 

![specific accuracy](https://user-images.githubusercontent.com/7085644/132602309-95258657-816c-477b-97bd-75f1acd50893.PNG)

The excess error generated from optimizing the empirical function is split into the approximation error, the estimation error, and the optimization error. 
Small-scale learning problems are not constrained by computing time, therefore the optimization error be made negligible to attain the best accuracy. 
On the other hand, large-scale learning problems have more training data, therefore the optimization error can be increased given the amount of computing power available. 

The following table shows that the SGD and 2SGD algorithms perform the best due to having the fastest times to find the expected risk, which is the most important factor for big data when compute time is the main constraint.

![realized that SGD is best for big data](https://user-images.githubusercontent.com/7085644/132602424-723211ed-cced-4726-9dd5-8818a5d6fd17.PNG)

The following diagram reveals how the stochastic gradient descent algorithm drastically outperforms the other algorithms in very little time and is only overtaken by TRON after the expected risk stops improving.

![results 1](https://user-images.githubusercontent.com/7085644/132602485-05395855-1570-4c02-b3c3-bce60b15ab8d.PNG)

The next two diagrams reveal how the other SGD variants (ASGD & SGDQN) perform even better compared to  CRF L-BFGS which took 72 minutes instead of a couple minutes to achieve the same results.

![results 2](https://user-images.githubusercontent.com/7085644/132602491-29a29d44-b014-471a-aaa2-86f409bff077.PNG)
![results 3](https://user-images.githubusercontent.com/7085644/132602497-8158b999-5ce0-470a-af9c-df4862a1f51d.PNG)

## TL;DR
* Small-scale machine learning is constrained by the number of training examples while large-scale machine learning is constrained by compute time, therefore large-scale algorithms have more room for the optimization accuracy tradeoff.
* For large scale machine learning, stochastic gradient descent algorithms should be used to achieve top accuracy in the fastest time.
* Second order stochastic gradient and average stochastic gradient perform the best on large scale datasets and can achieve efficiency after only a single run through the training data.
