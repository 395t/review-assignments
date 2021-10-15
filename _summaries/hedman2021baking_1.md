---
layout: summary
title: Summary
paper: {{hedman2021baking}}
# Please fill out info below
author: timchen0618
score: 8/10
---

TODO: Summarize the paper:

## What is the core idea?
NeRF is a good method to recreate 3D scenes from viewpoints unobserved by the system. However, it is computationally intensive and cannot be applied in real-time, since rendering one pixel would require evaluating MLP hundreds of times. Overall, the paper first reformulated the calculation of NeRF such that only 1 MLP operation is needed for constructing the image pixel in each ray. Then, they precomputed the values needed to construct NeRF and stored them in a structure called Sparse Neural Radiance Grid (SNeRG). With those, they achieved real-time rendering.


## How is it realized (technically)?
The original NeRF ...
We do not want to do so many MLP operations for one pixel, so we have to exchange storage for computation. 
But also, we do not want to precompute and store the entire 5D representation. 

### Deferred NeRF 
They reconstruct NeRF to output diffuse colors, volume densitise and 4-dimensional feature vectors. 

![image](https://user-images.githubusercontent.com/35536646/137429589-9c3df867-2e8f-4901-99a9-518cbfdfd33c.png)

They compute the color of a pixel following the steps below.

First, they calculate the accumulated diffuse color and feature vector along the ray. Then, the accumulated feature vector and the direction of the ray are passed into a MLP. The output of the MLP is considered a view-dependent residual, which is then added to the accumulated diffuse color.

![image](https://user-images.githubusercontent.com/35536646/137429557-43f72f38-2208-44d8-8009-1231e0852d16.png)



### Sparse Neural Radiance Grids (SNeRG)
They need to store diffuse colors, volume densities, and feature vectors. 
Instead of storing a dense voxel grid, they devised a block-sparse representation. 

**Macroblock: ** They used blocks of $$B^3$$ each to represent a densely occupied region. 
**Indirection Grid: ** Size of $$(N/B)^3$$, either indicates each macroblock is empty or points to the content of that macroblock in the 3D atlas.

### Rendering

![image](https://user-images.githubusercontent.com/35536646/137429651-083d3c62-f604-4828-a553-a07153f1e536.png)

For each pixel,

1. Match the ray through the indirection grid and ignore the empty ones
2. For non-empty macroblocks, fetch the precomputed values for all sample points along the ray.
3. Use alpha compositing to accumulate diffuse color and feature vectors, and stop if the opacity value saturated
4. With the accumulated values, we can compute the pixel color as in Eq. 7




* How well does the paper perform?
* What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
