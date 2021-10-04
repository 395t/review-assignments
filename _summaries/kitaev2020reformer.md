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
1. replace dot-product attentions with locality sensitive hashing bucketing to reduce the size of attention maps from $$O(L^2)$$ to $$O(L log L)$$.
2. use reversible residuals instead of the original residuals to disgard intermediate activations.

* How is it realized (technically)?

### Attention with locality sensitive hashing
The first simplification is enforcing identical Queries and Keys, so the linear layers used to project inputs can be reduced and buckets spread more evenly.
There is a key observation of the original original attention formulation: the softmax in $$\operatorname{softmax}\left(Q K^{T}\right)$$ is dominated by the largest terms in $$Q K^{T}$$.
By the first simplification, this observation reduces to partitioning the query set into nearest neighbors $$q_j \in Q$$ for each query $$q_i$$.

The authors introduce locality-sensitive hashing (LSH), an effective way to find such nearest neighbors quickly in high-dimensional spaces.
An LSH is defined as a hash function that assigns the same hash exclusively to nearby vectors with high probability.
The specific hash function that the author choose is an angular locality sensitive hashing, which is defined as $$h(x)=\arg \max ([x R ;-x R])$$, where R is a random projection matrix.

The key idea of this scheme is to first project vectors on a unit sphere and then divide the space into cardinal sectors as buckets by comparing the the coordinate numbers.
A figure on simplified 2D case for LSH is shown below.
Once points are on the circle, whether coordinate $$x_0 > x_1$$ and $$ -x_0 > x_1$$ defines the two diagonal lines and therefore separates the space into four sectors -- four buckets.
![F76EC8AB-A423-4993-A77C-E79FF4A01917](https://user-images.githubusercontent.com/25853995/135883728-d0e7f6f7-5648-4601-a4d3-98d92b730650.png)

Now that we have a working LSH, the equivalence relations given by the LSH would partition vectors into serveral buckets, where only intra-bucket attention computation is significant enough.
There is one last optimization for better implementation on gpu and peak memory reduction: batching and chuncking.
The queries are sorted by LSH results into buckets and the queries are chopped into even size chuncks.
To fully cover attentions in the same LSH partition, the attentions are calculated within the current chunck and the previous chunck.
The sorting, batching and chuncking process is shown in the figure below.
![A80E76C1-BB64-4968-82E1-C71DA8485BCF](https://user-images.githubusercontent.com/25853995/135887076-6d0d95fd-13d6-4a63-9941-f3551ddf4328.png)

Such approximation reduces the memory consumption as well as the computation time from square to nearly linear, which concludes the first part of the improvement.

### Reversible residuals

When stacking multiple layers of transformers, the intermediate activations still consume a lot of memory, which are necessary for back-propagation.
The authors propose to use the reversible residuals in order to recover the pre-image from the output and therefore eliminate the necessity of storing pre-images for back-propagation.
Technically, the reversible residual networks work as linear systems with intertwined variables to enable simple additive/substractive solutions for pre-images.
Original ResNet can be formulated as $$ y = x + F(x) $$ and reversible Resnet operates on paris of input/output as $$(x_1, x_2) \mapsto (y_1, y_2)$$.
Specifically, the forward pass can be defined as $$ y_{1}=x_{1}+F\left(x_{2}\right) \quad y_{2}=x_{2}+G\left(y_{1}\right) $$ and the pre-images can be easily obtained by $$ x_{2}=y_{2}-G\left(y_{1}\right) \quad x_{1}=y_{1}-F\left(x_{2}\right) $$.
For the application in transformer, the reversible residuals are realized as $$Y_{1}=X_{1}+\text { Attention }\left(X_{2}\right) \quad Y_{2}=X_{2}+\text { FeedForward }\left(Y_{1}\right)$$.

Therefore, the proposed method eliminate the memory consumption of storing the intermediate activations for back-propagation.


* How well does the paper perform?

In short, the proposed method performs on par with the original transformer when parameter sizes are fixed the same.

Firstly, the authors examine the performance of whether to share queries and keys.
As shown below, such choice has no impact on the performance.
![735460CC-6FEE-41CF-B361-D9777FBB71C7](https://user-images.githubusercontent.com/25853995/135893910-5be49c58-9e9a-47f6-9397-c8d107a3a6f2.png)

Then, the authors compare the original residuals against the reversible residuals.
Again, no performance gap is found.
![F018B332-26E0-4B74-8937-3858B0ECB957](https://user-images.githubusercontent.com/25853995/135894077-226037d1-c5a7-44f5-ada7-ae2693ee0b55.png)

Finally, the authors compare the proposed method against previous methods with the same parameter size, and the evaluation performace has no significant difference.
![ED6EC1A2-08FB-46E5-99EE-039F37B79EAE](https://user-images.githubusercontent.com/25853995/135894357-79bcf286-5ef0-498b-8fc7-4fc75cd28cd8.png)


* What interesting variants are explored? 

The authors explore the implementation for chuncking and batching. 
Since the transformer is basically a temporally decoupled sequence model, it was designed to operate parallelly across the temporal dimension.
Therefore, it enables chunking the model into smaller batches to train models operating on very long sequences without overwhelming the memory.
In this work, the authors explore techniques to apply chuncking and batching on the proposed method as well, which successfully extends the transformer to train and operate on extremely long sequences in some scenarios.

Additionally, the authors propose multi-round LSH for more stable and accurate identifications of nearest neighbors to alleviate the probabilistic nature of LSH.


## TL;DR
- Attentions in transformers consume $$O(L^2)$$ of memory and computation but are mostly sparse due to the dominance in softmax.
- Apply locality-sensitive hashing to partition queries with nearest neighbors and only calculate the dominant terms in softmax to reduce calculations to nearly linear.
- Replace original residual layers with the reversible residual layers and save memory from storing intermediate activation results.




