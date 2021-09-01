---
layout: summary
title: Summary
paper: Maxout Networks
# Please fill out info below
author: specfazhou
score: 5
---

TODO: Summarize the paper:

* What is the core idea? <br/>
This paper comes up with a new function -- maxout function. Using Maxout function together with dropout techniques can classify images with lowest error rate on several well-known images dataset at that time. 

* How is it realized (technically)? <br/>
the input is a **d**-dim vertical vector, **X=(x_1,x_2,...x_d)^{t}**) with outputs **m**-dim vertical vector **h = (h_1,h_2,...,h_m)^{t}** in the next layer. Choose an integer **k**, and what the maxout function does is equivalent to adding another layer in between with **k** x **m** units, which forms a matrix **Z = (z_{i,j}**) where **0<i<k+1, 0<j<m+1**. Then, the **j**-th column of **Z** is **W(: , :, j)X**, where **W** is a **k** x **d** x **m** tensor with elements are parameters, and **h_j** is the maximum element in the **j**-th column of **Z**.      

* How well does the paper perform?<br/>
On MNIST, CIFAR-10, CIFAR-100, SVHN these four datasets, the neural networks that use maxout function and dropout techique lower the error rate compare to previous works. Especially on CIFAR-100, it reduced error rate from 42.51% to 38.57%. Although in some cases, the way they preprocess datas, and the size of models they use are different, they did comparison experiments to show Maxout function is the reason for better performance. 

* What interesting variants are explored?<br/>
It seems this paper only focuses on the maxout function, and mainly discuss how well it performed together with dropout technique.  

## TL;DR
* Three
* Bullets
* To highlight the core concepts<br/>
1. The maxout function has parameters can be learned, that's very different from traditional activication function like softmax, and sigmoid. <br/>
2. With two maxout layers, one can approximate any continuous function on closed and bounded subset of **R^d**, and one maxout layer can approximate linearly piecewise function<br/>
3. Compare to max{a,0} function, maxout function seems make the computer easier to do backpropagation.<br/>
**These are three things I like about the maxout function (paper)**
