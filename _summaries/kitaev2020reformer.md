---
layout: summary
title: Summary
paper: kitaev2020reformer
# Please fill out info below
author: liyanc
score: 8
---


* What is the core idea?

The authors propose a new transformer to improve the memory efficiency of the original transformer, named as reformer. 
The core idea includes two aspects: 
use reversible residuals instead of the original residuals to disgard intermediate activations; 
replace dot-product attentions with locality sensitive hashing to reduce the size of attention maps from $$O(L^2)$$ to $$O(L log L)$$.

* How is it realized (technically)?

### Attention with locality sensitive hashing
The first simplification is enforcing identical Queries and Keys, so the linear layers used to project inputs can be reduced.
There is a key observation of the original original attention formulation: $$\operatorname{softmax}\left(Q K^{T}\right)$$ is a softmax and therefore dominated by the largest terms in $$Q K^{T}$$.
By the first simplification, this observation reduces to finding the nearest neighbors $$q_j \in Q$$ for each query $$q_i$$.

The authors introduce locality-sensitive hashing (LSH), an effective way to find such nearest neighbors quickly in high-dimensional spaces.
An LSH is defined as a hash function that assigns the same hash exclusively to nearby vectors with high probability.
The specific hash function that the author choose is an angular locality sensitive hashing, which is defined as $$h(x)=\arg \max ([x R ;-x R])$$, where R is a random projection matrix.

The key idea of this scheme is to first project vectors on a unit sphere and then divide the space into cardinal sectors as buckets by comparing the the coordinate numbers.
A figure on simplified 2D case for LSH is shown below.
Once points are on the circle, whether coordinate $$x_0 > x_1$$ and $$ -x_0 > x_1$$ defines the two diagonal lines and therefore separates the space into four sectors -- four buckets.
![F76EC8AB-A423-4993-A77C-E79FF4A01917](https://user-images.githubusercontent.com/25853995/135883728-d0e7f6f7-5648-4601-a4d3-98d92b730650.png)


### Reversible residuals


* How well does the paper perform?
* What interesting variants are explored? 


## TL;DR
- point1
- point2
- point3

