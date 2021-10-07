---
layout: summary
title: Summary
paper: liu2021swin 
# Please fill out info below
author: ywen666
score: 9
---

## Abstract
* Transformer is designed for text domain. The high resolution of pixels in images prevent smooth application of transformer in visual domain. 
* Semantic segmentation that require dense prediction at the pixel level, and this would be intractable for Transformer ($$O(n^2)$$).
* This paper proposed to a hierarchical Transformer whose representation is computed with shifted windows (SWIN). 
* By limiting self-attention computation to non-overlapping local windows while also allowing for cross-window connection, SWIN has linear computational complexity with respect to image size. 
* Ultimate goal: expand the applicability of Transformer such that it can serve as a general-purpose
backbone for computer vision, as it does for NLP and as CNNs do in vision. 

## Motivation
To reduce complexity, Swin Transformer constructs a hierarchical representation by starting from small-sized patches (outlined in gray) and gradually merging neighboring patches in deeper
Transformer layers. 

<img width="650px" src="liu2021swin_2a.png"/>  

The linear computational complexity is achieved by computing self-attention locally within non-overlapping windows that partition an image (outlined in red). The number of patches in each
window is fixed, and thus the complexity becomes linear to image size.

A key design element of Swin Transformer is its shift of the window partition between consecutive self-attention layers. The shifted windows bridge the windows of the preceding layer, providing connections among them that significantly enhance modeling power. 

<img width="650px" src="liu2021swin_2b.png"/>  

## Overall Architecture

Swin Transformer first splits an input RGB image into non-overlapping patches by a patch splitting module. Each patch is treated as a “token” and its feature is set as a concatenation of the raw pixel RGB values. A linear embedding layer is applied on this raw-valued feature to project it to an arbitrary dimension (denoted as C).

Swin Transformer blocks are applied on these patch tokens. The Transformer blocks maintain the number of tokens ($$\frac{H}{4} \times \frac{W}{4}$$), and together with the linear embedding are referred to as “Stage 1”.

The first patch merging layer concatenates the features of each group of 2 × 2 neighboring patches, and applies a linear layer on the 4C-dimensional concatenated features. This reduces the number of tokens by a multiple of 2×2 = 4 (2× downsampling of resolution), and the output dimension is set to 2C. Swin Transformer blocks are applied afterwards for feature transformation, with the resolution kept at $$\frac{H}{8} \times \frac{W}{8}$$. This first block of patch merging
and feature transformation is denoted as “Stage 2”.

<img width="650px" src="liu2021swin_2c.png"/>  

## Shifted Window based Self-Attention
### Self-attention in non-overlapped windows

## Experiements