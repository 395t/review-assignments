---
layout: summary
title: Summary
paper: {{hedman2021baking}}
# Please fill out info below
author: timchen0618
score: 8/10
---

## What is the core idea?
NeRF is a good method to recreate 3D scenes from viewpoints unobserved by the system. However, it is computationally intensive and cannot be applied in real-time, since rendering one pixel would require evaluating MLP hundreds of times. Overall, the paper first reformulated the calculation of NeRF such that only 1 MLP operation is needed for constructing the image pixel in each ray. Then, they precomputed the values needed to construct NeRF and stored them in a structure called Sparse Neural Radiance Grid (SNeRG). With those, they achieved real-time rendering.


## How is it realized (technically)?

To reduce computation, we do not want to do so many MLP operations for one pixel, so we have to trade computation for storage. 
But also, we do not want to precompute and store the entire 5D representation. (Too memory intensive)

What they do is a hybrid approach which precomutes some value in a sparse 3D space and leave some computation to inference time. 

### Deferred NeRF 
They reconstruct NeRF to output diffuse colors, volume densitise and 4-dimensional feature vectors. 

![image](https://user-images.githubusercontent.com/35536646/137429589-9c3df867-2e8f-4901-99a9-518cbfdfd33c.png)

They compute the color of a pixel following the steps below.

First, they calculate the accumulated diffuse color and feature vector along the ray. Then, the accumulated feature vector and the direction of the ray are passed into a MLP. The output of the MLP is considered a view-dependent residual, which is then added to the accumulated diffuse color.

![image](https://user-images.githubusercontent.com/35536646/137429557-43f72f38-2208-44d8-8009-1231e0852d16.png)

This deferred version of NeRF requires only 1 MLP evaluation per pixel. (In contrast to hundreds of samples as in standard NeRF.)


### Sparse Neural Radiance Grids (SNeRG)
They need to store diffuse colors, volume densities, and feature vectors. 
Instead of storing a dense voxel grid, they devised a block-sparse representation. 

**Macroblock:** They used blocks of $$B^3$$ each to represent a densely occupied region. 
**Indirection Grid:** Size of $$(N/B)^3$$, either indicates each macroblock is empty or points to the content of that macroblock in the 3D atlas.

### Rendering

![image](https://user-images.githubusercontent.com/35536646/137429651-083d3c62-f604-4828-a553-a07153f1e536.png)

For each pixel,

1. Match the ray through the indirection grid and ignore the empty ones
2. For non-empty macroblocks, fetch the precomputed values for all sample points along the ray.
3. Use alpha compositing to accumulate diffuse color and feature vectors, and stop if the opacity value saturated
4. With the accumulated values, we can compute the pixel color as in Eq. 7


### Other Tricks & Details
**Regularization:** To enable block-sparse representation mentioned previously and reduce rendering time and storage, they introduce opacity regularization. This essentially encourages sparsity in NeRF's opacity fields. Regularization is done by penalizing predicted density. 

![image](https://user-images.githubusercontent.com/35536646/137430839-8723c8ac-028c-4c82-876a-5de081fd1134.png)


**Sparsification:** They also further sparsify the voxel grid by culling macroblocks with low opacity and visibility.

**Compresssion:** Represent all values with only 8 bits; compress a indirection grid as a lossless PNG and 3D atlas as a set of lossless PNGs, a set of JPEGs or a video encoded with H264.

## How well does the paper perform?
They experiment with the proposed method on free-viewpoint rendering of 360-degree scenes. The quality of their model is comparable to other methods, yet the runtime is significantly faster. 

![image](https://user-images.githubusercontent.com/35536646/137431571-07e17268-7abf-4dc3-9c9e-6ef0e8822b25.png)


## What interesting variants are explored?
They offer some interesting ablation studies regarding their design decisions. 
![image](https://user-images.githubusercontent.com/35536646/137432718-fbeafe75-c180-4cc1-819a-79c97c8cb8a8.png)

Table 2. basically shows that using a smaller network (Tinyview) and deferred NeRF do hurt performance. Using compression schemes also displayed similiar effect. But these are just crucial parts to speeding up the inference time, and the performance drops are not too significant. 

![image](https://user-images.githubusercontent.com/35536646/137432701-f7490333-5054-4b70-937b-f18ed191e91c.png)

Table 3. showed the compression techniques do reduce memory usage. For example, H264 reduce storage by 200x and sacrifice little performance.


## TL;DR
- NeRF is great method for view synthesis, but it cannot be applied real-time. They proposed a deferred version of NeRF and store precomputed values in structure called Sparse Neural Radiance Grid (SNeRG) to speed up. 
- Specifically, SNeRG uses a sparse voxel grid to store precomputed values of a scene, and the view-dependent residuals are computed and added at inference time. 
- They achieved real-time image rendering without much performance loss compared to baseline methods.


