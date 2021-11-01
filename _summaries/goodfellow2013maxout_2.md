---
layout: summary
title: Summary
paper: goodfellow2013maxout
# Please fill out info below
author: specfazhou
score: 5
---

TODO: Summarize the paper:

* What is the core idea? <br/>
This paper comes up with a new function -- maxout function, which has parameters that can be learned. Authors believe that models using maxout functions can exhabit the true power of dropout. It is more than just a technique slightly increase performance of other networks or an approximation used in neural networks. 

* How is it realized (technically)? <br/>
the input is a **d**-dim vertical vector, **X=(x_1,x_2,...x_d)^{t}**) with outputs **m**-dim vertical vector **h = (h_1,h_2,...,h_m)^{t}** in the next layer. Choose an integer **k**, and what the maxout function does is equivalent to adding another layer in between with **k** x **m** units, which forms a matrix **Z = (z_{i,j}**) where **0<i<k+1, 0<j<m+1**. Then, the **j**-th column of **Z** is **W(: , :, j)X**, where **W** is a **k** x **d** x **m** tensor with elements are parameters, and **h_j** is the maximum element in the **j**-th column of **Z**.      

* How well does the paper perform?<br/>
On MNIST, CIFAR-10, CIFAR-100, SVHN these four datasets, the neural networks that use maxout function and dropout techique lower the error rate compare to previous works. Especially on CIFAR-100, it reduced error rate from 42.51% to 38.57%. On MNIST, it reduced error rate from 0.47% to 0.45%. On CIFAR-10, although there is a neural network outperform maxout+dropout without data augmentation, but maxout+dropout+data augmentation network still yield the best result, which has error rate 9.38%. On,SVHN, it reduced error rate from 2.68% to 2.47%. Although in some cases, the way they preprocess datas, and the size of models they use are different, they did comparison experiments to show Maxout function is the reason for better performance.

* What interesting variants are explored?<br/>
It seems this paper only focuses on the maxout function, and mainly discuss how well it performed together with dropout technique. However, one interesting fact is that maxout network with two hidden layers can approximate every continuous function. It is an efficient approximator.  

## TL;DR
* Three
* Bullets
* To highlight the core concepts<br/>
1. The maxout function has parameters can be learned, that's very different from traditional activication function like softmax, and sigmoid. <br/>
2. With two maxout layers, one can approximate any continuous function on closed and bounded subset of **R^d**, and one maxout layer can approximate linearly piecewise function<br/>
3. Maxout function is way better than rectifiers<br/>
**These are three things I like about the maxout function (paper)**
