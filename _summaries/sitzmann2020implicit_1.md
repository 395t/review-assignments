---
layout: summary
title: Summary
paper: sitzmann2020implicit_1
# Please fill out info below
author: rll2396
score: 7
---

TODO: Summarize the paper:
* Background
    * Implicit functions take the form $$F(x, \Phi, \nabla_x\Phi, \nabla_x^2\Phi, \dots) = 0$$
        * $$\Phi$$ maps $$x$$ to some quantity of interest
        * e.g. the equation for the unit circle is $$x^2 + \Phi^2 - 1 = 0$$
    * Traditional methods for modeling such functions involve discretizing the domain into sections, then numerically solving at each section
    * NNs can be used for continuous model
        * agnostic to grid resolution
        * model memory only scales with complexity of the function, rather than spatial resolution
        * common activation functions such as ReLU achieve poor performance
* What is the core idea?
    * Two main contributions
        * demonstrate that the sine activation functions works very well for creating implicit neural representations
        * create a new initialization technique, which is essential for the performance that they achieve with their network
* How is it realized (technically)?

    ![Architecture](sitzmann2020implicit_1a.png)

    * Implicit equations relate an input, a function, and the function's derivatives to 0
        * a simple loss function is just absolute value of the relation
        * loss calculated at random points in the domain and summed up
    * Sinusoidal representation network (SIREN)
        * MLP with sine as the activation function
        * during initialization, weights are drawn from $$U(-\sqrt{\frac{6}{n}},\sqrt{\frac{6}{n}})$$
            * $$n$$ is input dimension
    * For all experiments, they use a 5-layer MLP and optimize it using ADAM with a learning rate of 1e-4

* How well does the paper perform?

    ![Poisson](sitzmann2020implicit_1c.png)

    ![Poisson](sitzmann2020implicit_1f.png)

    * Poisson image reconstruction
        * SIREN is used to solve the Poisson equation
        * goal is to reconstruct an image
        * the gradient or Laplacian of the ground truth image is used for supervision
    * Poisson image editing
        * SIREN is used to create an image from the linear interpolation of the gradients of two images

    ![SDFs](sitzmann2020implicit_1b.png)

    * Representing shapes with signed distance functions
        * SDF outputs the distance to the boundary of the shape
        * the SDF values are negative when outside the shape and positive when inside the shape
        * gradient is $$1$$ almost everywhere
        * distance values on the shape should be close to 0
        * distance values off the shape should not be close to 0
        * for calculating loss, sample random points in the domain, half on the shape half off it

    ![Helmholtz](sitzmann2020implicit_1e.png)

    * Helmholtz equation
        * Supervise with loss function based on helmholtz equation, which relates the Laplacian of a function with itself

    ![CelebA](sitzmann2020implicit_1d.png)

    * Learning a space of implicit functions
        * convolutional encoder maps partial observations of an image to latent code vectors
        * ReLU hypernetwork maps the latent code vectors to SIREN network parameters
        * the resulting SIREN can fill in the rest of the image


## TL;DR
* Sine activation functions are effective at modeling implicit problems
* Requires careful initialization
* Demonstratably achieves much better performance on a variety of tasks
