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
This paper comes up with a new function -- maxout function. 
* How is it realized (technically)? <br/>
the input is a **d**-dim vertical vector, **X=(x_1,x_2,...x_d)^{t}**) with outputs **m**-dim vertical vector **h = (h_1,h_2,...,h_m)^{t}** in the next layer. Choose an integer **k**, and what the maxout function does is equivalent to adding another layer in between with **k** x **m** units, which forms a matrix **Z = (z_{i,j}**) where **0<i<k+1, 0<j<m+1**. Then, the **j**-th column of **Z** is **W(: , :, j)X**, where **W** is a **k** x **d** x **m** tensor with elements are parameters, and **h_j** is the maximum element in the **j**_th column of **Z**.      
* How well does the paper perform?

* What interesting variants are explored?
* 

## TL;DR
* Three
* Bullets
* To highlight the core concepts

