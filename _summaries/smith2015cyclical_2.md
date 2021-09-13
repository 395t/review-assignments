---
layout: summary
title: Summary
paper: smith2015cyclical
# Please fill out info below
author: liyanc
score: 5
---

* What is the core idea?

    The author proposed a method to for adaptively controlling learning rate in order to eliminate the manual tuning of learning rate and significantly improve the convergence speed.
Common methods require manual tuning of the learning rate and such empirical tuning has significant impact on the model convergence speed as well as the performance.
Additionally, popular exponential decay of the learning rate requires longer training time and introduces another empirical tuning parameter.

    Therefore, this paper proposed an adaptive search and decay of learning rates waiving empirical trials.
The proposed method builds on the observation that larger learning rates improve short-term results while smaller learning rates benefit long term results (specifically model generalizability, albeit not mentioned by the author).
As a result, a cyclic sweeping learning rate can take advantage of both worlds.

* How is it realized (technically)?

  Essentially, the author proposed to sweep the learning rate back and forth within a range as shown in the the figure. 
  ![114D5709-A3EF-4F6F-930C-90088E4F9FC8](https://user-images.githubusercontent.com/25853995/133025348-eb1884d9-d4ba-4e65-bd31-a48a8bef0dbc.png)
  
  As for the shape of swing (triangular, parabolic, sinusoidal), the author suggests that empirical results show it irrelavent.
  
  There are two key considerations for this method: how to find the step size and how to determine the appropriate range for the swing.
  - The optimal step size should cover 2-10 epoches.
  - Perform a set of linear scanning of learning rates for training and locate a resonable range from the scanning result as shown in an example on CIFAR-10 

![3F0AD94F-DD63-4B9B-BA79-9C9AB0556100](https://user-images.githubusercontent.com/25853995/133025837-a8bd2bed-2628-44e3-829a-5cc2e83ee539.png)


* How well does the paper perform?

  The author first validates and analyzes the method on CIFAR-10 dataset. 
  The test accuracy for each training protocol is shown in the figure, which demonstrates that the proposed method achieved an optimal performance with significantly shorter training time.
  ![75769D57-5F95-4511-AE9C-B6D328D0D3E4](https://user-images.githubusercontent.com/25853995/133026139-32b5fb24-5513-4a67-9a2f-c2144100cf2c.png)
  In order to invalidate the hypothesis that only the smaller end of learning rates contribute to the performance, the author designed a decay protocol to decay the learningrate within the first stepsize and fix it to the end.
  The result is inferior and therefore shows that either large or small learning rates along couldn't achieve the performance, but the cyclic sweeping characterastics achieve the result.
  ![AD57D510-CEA2-4A9F-A17D-C1A190F4DCA3](https://user-images.githubusercontent.com/25853995/133026750-42727a97-35f2-446f-890c-89c5d6c09fcf.png)
  
  The author performed experiments on CIFAR-100 dataset with ResNet, Stochastic Depth, and DenseNet as well. 
  The proposed method demonstrates a similar edge over other baselines.
  The table shows the results of baselines starting at three different learning rates and the proposed sweeping learning rate.
  ![F735DB53-5E76-4F4E-BE45-105DD6A55D05](https://user-images.githubusercontent.com/25853995/133027080-bf7fa145-38d1-482c-ae65-a0561bf9ea7c.png)

  Finally, the author performed training and tests on ImageNet with AlexNet and GoogleNet. All the results show the proposed method gives a lead over the baseline in terms of the final performance and the convergence speed.
  ![C35B5192-1ED0-471B-ABF1-EC3A02C2D03D](https://user-images.githubusercontent.com/25853995/133028556-0b000db3-a840-4934-a2f0-0420c73182c3.png)
  
  Note that the experiments are all perfomed on relatively small datasets with the simple task for classification, the conclusion might not well generalize to today's work.
  This proposed method could potentially improve the generalizability of trained models according to more recent works since it's likely that sweeping learning rates leads to "flatter" minimas, which would imply better generalizability.
  It would be interesting to see follow-up works with further analysis with this respect.
 

## TL;DR
* Sweeping learning rates within a range can take advantage of both large learning rates and small learning rates.
* Step size should cover 2-10 epoches, and the range should be determined by pre-scanning over possible ranges.
* Cyclic learning rates show a significant improvement on relatively small datasets for image classification.
