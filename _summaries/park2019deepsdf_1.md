---
layout: summary
title: Summary
paper: {{paper_tag}}
# Please fill out info below
author: patelojas
score: # How did you like this paper 0(dislike) to 10(love)
---

# Core Idea

DeepSDF represents an approach to represent 3D geometryies for rendering and reconstruction and is a novel aproach to generative 3D modeling. Other approaches face a similar trade-off across fidelity, efficiency, and compression capabilities. DeepSDF is a learned continuous Signed Distance Function that represents a class of shapes that enables high quality shape representation, interpolation, and completion from partial and noisy 3D input data. It represents a shape's surface by a continuous volumetric field. It uses the magnitude of a point in the field to represent the distance to the surface boundary and uses the sign to indicate whether the region is inside or outside of the shape.

# Difference Between Classical SDF

Classical SDF typically represents the surface of a single shape, but DeepSDF can represent an entire class of shapes. 

# Technical Implementation

DeepSDF is a continuous shape learning approach. The authors describe modeling shapes as the zero iso-surface decision boundaries of feed-forward networks trained to represent SDFs. They use a signed function, which is a continuous function that outputs a point's distance to the closest surface who's sign encodes whether the point is inside or outside of the surface. The surface is represented by SDF(*) = 0. This is used to predict the SDF value of a given query position to then extract the zero level-set surface. 

$$ SDF(x) = s: x \in R^3, s \in R $$

The most direct way to use this approach is to train a single deep network for a given shape. To then generate the 3D model, they use a feed-forward network composed of 8 fully connected layers with dropouts. 

However, training a netwrok for each shape is not practical. A better approach is to create a model that can represent a wide variety of shapes in a low dimensional latent space. 

# Performance

<img src="park2019deepsdf_1a.png"/>

A number of experiments were conducted to show the representational power of DeepSDF. The metrics were both in terms of its ability to describe geometric details and its generalization capabilitiy to learn a desirable shape embedding space. Four experiments were proposed to test its ability to represent training data, use learned feature representation to reconstruct unseen shapes, apply shape priors to complete partial shapes, and learn smooth and complete shape embedding space from which we can sample new shapes. The ShapeNet dataset was used. 

For representing known 3D shapes, the results are shown below. DeepSDF significantly beats OGn and AtlasNet in Chamfer distance.

<img src="park2019deepsdf_1b.png"/>

In representing unknown 3D shapes, DeepSDF again beats AtlasNet. AtlasNet performs well on shapes that have no holes, but struggles with shapes like chairs that have holes. 

<img src="park2019deepsdf_1d.png"/>

DeepSDF also produces more visually pleasing and accurate shape reconstructions than other methods. 

<img src="park2019deepsdf_1c.png"/>


## TL;DR
* DeepSDF is an adjustment on classical SDF for shape representation and completion
* Can represent complex topologies, closed surfaces, and provide a high quality wsurface of a normal shape
* Outperforms the applicable benchmarked methods for its tasks