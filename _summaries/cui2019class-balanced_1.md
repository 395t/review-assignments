---
layout: summary
title: Summary
paper: cui2019class-balanced
# Please fill out info below
author: # Your GitHub id
score: # How did you like this paper 0(dislike) to 10(love)
---

### Class Imbalance Problem
![](cui2019class-balanced_1a.png)
### Effective Number of Samples
![](cui2019class-balanced_1b.png)
### Class-Balanced Loss (CB Loss)
![](cui2019class-balanced_1c.png)
![](cui2019class-balanced_1d.png)
### Experimental Results
![](cui2019class-balanced_1e.png)
![](cui2019class-balanced_1f.png)

## TL;DR
* The paper tackles the problem of long-tailed data distribution where a few classes account for most
of the data, while most classes are under-represented.
* The paper provides a theoretical framework to study the effective number of samples and show how to design a class-balanced term to deal with long-tailed training data.
* The paper shows that significant performance improvements can be achieved by adding the proposed class-balanced term to existing commonly used loss functions including softmax cross-entropy, sigmoid cross-entropy and focal loss.