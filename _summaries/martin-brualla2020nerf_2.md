---
layout: summary
title: Summary
paper: martin-brualla2020nerf
# Please fill out info below
author: nilesh2797
score: 8
---

## What is the core idea?
* NeRF works well on images of static subjects captured under controlled settings but it fails to model real-world variabilities such as  illumination or transient occluders
* NeRF-W (this paper) extends NeRF to address these issues and is able to render accurate reconstructions from unstructured image collections taken from the internet!
<p align="center"><img src="martin-brualla2020nerf_2/nerf-w-demo.gif"/> <img src="martin-brualla2020nerf_2/nerf-w-demo-2.gif"/></p>

## How is it realized (technically)?
### Latent appearance modelling
* To adapt to the various lighting and camera settings, NeRF-W learns a separate low-dimensional "appearance" embedding for each of the training image.
* The appearance embedding is only fed to the MLP which gives out the color but not to the MLP which estimates the density, this ensures that the 3-D geometry is shared across all training images of a scene
## How well does the paper perform?
## What interesting variants are explored?

## TL;DR
* Three
* Bullets
* To highlight the core concepts
