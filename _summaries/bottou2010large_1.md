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

A model's performance can be measured either with empirical risk, En(f), which is the effectiveness of the model on the training set:

![empirical risk](https://user-images.githubusercontent.com/7085644/133015130-fbdb9bf5-8fd6-46f4-a4b8-eec3f4b82714.PNG)

Or it can be measured with expected risk, E(f), which is the effectiveness of the model on future data:

![expected risk](https://user-images.githubusercontent.com/7085644/133015208-5b9aa61b-7c92-4aed-acf4-0d4ccfe6225f.PNG)

Gradient descent updates the weights using the entire training set with the following formula and has been previously cited as a good algorithm to minimize the empirical risk.

![gradient descent](https://user-images.githubusercontent.com/7085644/133016516-d182cec0-3d06-4832-aac9-61f255deec74.PNG)

In comparison, stochastic gradient descent (SGD) randomly chooses one datapoint to calculate the gradients at each iteration rather than considering the whole dataset to reduce the computational cost.

![SGD](https://user-images.githubusercontent.com/7085644/132602146-a90027db-61db-4ad7-8a6f-1d2f72966bcc.PNG)

The function, f*, represents the best prediction function that we can obtain given our start to SGD.
Therefore, we let F encompass the family of functions acquired during SGD from the chosen parameters where f* is the function that minimizes E(f).
Finding the empirical risk optimum can be costly, therefore the iterations are stopped once a specific accuracy is reached. 

![specific accuracy](https://user-images.githubusercontent.com/7085644/132602309-95258657-816c-477b-97bd-75f1acd50893.PNG)

The excess error generated from optimizing the empirical function is split into the approximation error, the estimation error, and the optimization error. 
With these three areas for error, a tradeoff exists between the optimization accuracy, the family of functions size, and size of the dataset.
Small-scale learning problems are not constrained by computing time, therefore the optimization error can be made negligible to attain the best accuracy. 
On the other hand, large-scale learning problems have more training data, therefore the optimization error can be increased given the amount of computing power available. 

The following table shows that the SGD and 2SGD algorithms perform the best due to having the fastest times to find the expected risk, which is the most important factor for big data when compute time is the main constraint.

![realized that SGD is best for big data](https://user-images.githubusercontent.com/7085644/132602424-723211ed-cced-4726-9dd5-8818a5d6fd17.PNG)

The following diagram reveals how the stochastic gradient descent algorithm drastically outperforms the other algorithms in very little time and is only overtaken by TRON after the expected risk stops improving.

![results 1](https://user-images.githubusercontent.com/7085644/132602485-05395855-1570-4c02-b3c3-bce60b15ab8d.PNG)

The next two diagrams reveal how the other SGD variants (ASGD & SGDQN) perform.
In the following graphs, averaged stochastic gradient descent (ASGD) achieves optimal expected risk in only one iteration.

![results 2](https://user-images.githubusercontent.com/7085644/132602491-29a29d44-b014-471a-aaa2-86f409bff077.PNG)

The following graphs reveal how single second order stochastic gradient pass (SGDQN) performs best for a CRF and the paper reports that all three SGD algorithms outperform the CRF L-BFGS optimizer which took 72 minutes instead of a couple minutes to achieve the same results.

![results 3](https://user-images.githubusercontent.com/7085644/132602497-8158b999-5ce0-470a-af9c-df4862a1f51d.PNG)

## TL;DR
* For large-scale machine learning, stochastic gradient descent algorithms should be used to achieve good accuracy in the fastest time compared to gradient descent algorithms.
* Large-scale machine learning accuracy can be broken down and measured with the approximation error, the estimation error, and the optimization error, which poses a tradeoff between the optimization accuracy, the size of the training data, and the size of the family of prediction functions.
* Small-scale machine learning is constrained by the number of training examples while large-scale machine learning is constrained by compute time, therefore large-scale algorithms have more room for the optimization accuracy tradeoff.
