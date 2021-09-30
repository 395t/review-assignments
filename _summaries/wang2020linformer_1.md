---
layout: summary
title: Summary
paper: {{paper_tag}}
# Please fill out info below
author: TongruiLi # Your GitHub id
score: 10# How did you like this paper 0(dislike) to 10(love)
---

* What is the core idea?

The main contribution of the paper is that it is able to approximate self-attention by a low rank martrix, thus enabling the complexity to reduce from $$O(n^2)$$ to $$O(n)$$. This outperforms the previous state of art of Reformer (Kitaev et al. 2020), which uses $$O(n log(n))$$ complexity.

![complexity](wang2020linformer_1a.png)


* How is it realized (technically)?
Recall multi head attention holds the following formulation:

$$Multihead(Q, K, V) = Concat(head_1, head_2, ..., head_h)W^O$$

Q, K, V are $$nxd_m$$ matricies.

We can define a low rank matrix $$\widetilde{P}$$ such that the following therom is true:

![therom1](wang2020linformer_1c.png)

We can establish the above proof by first using the union bound and later the Johnson–Lindenstrauss lemma.

![therom1proof](wang2020linformer_1b.png)

We can the use the above fact to perform **SVD** on $$\widetilde{P}$$ to get the approximated contextual mapping matrix

By choosing a small projection dimension $$k$$, we can reduce the time and space complexity to $$O(nk) \simeq O(n)$$ with small error.

![therom2result](wang2020linformer_1d.png)

* How well does the paper perform?
![timeresult](wang2020linformer_1e.png)

![convergenceresult](wang2020linformer_1f.png)

In term of efficiency, the linformer is able to achieve a high speed up coeffcient, esspecially when sequence length is high. 

In term of convergence, though the matrix is approximated, the paper is able to demonsrate convergence regardless of the sequence length.


## TL;DR
* It is possible to approximate transformer matrixs in $$O(n)$$ time

* The approximate only grants a small error, and is efficient especially in high length sequence data

* Convergence property is not affected by the approximation