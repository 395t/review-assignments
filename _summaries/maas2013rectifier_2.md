---
layout: summary
title: Rectifier Nonlinearities Improve Neural Network Acoustic Models, Maas, Hannun, Ng; 2013
paper: 	maas2013rectifier
# Please fill out info below
author: sritank
score: 8/10
---

TODO: Summarize the paper:
* What is the core idea?
DNNs with ReLU and other non-sigmoid activation functions had performed much better on image recognition and text classification tasks. So the paper explores using DNNs for building acoustic models and how different rectifier non-linearities can improve accuracy of the acoustic model.

* How is it realized (technically)?
The authors train the DNN model for an LVCSR (large vocabulary continuous speech recognition) task. To study the impact of different non-linearities on the training accuracy, they do not use regularization or pre-trained weights for the network. 

For the same speech recognition task, they replace the GMM/HMM acoustic model with a DNN. The DNN inputs are the same as the GMM it replaces, i.e. MVCC features of the audio signal. The output of the DNN is the senone likelihood probability function. They train DNNs (2-4 layers containing 2048 units/layer) containing sigmoid, ReLU and Leaky ReLU activation functions using stochastic gradient descent. 



* How well does the paper perform?
They evaluated the WER and cross entropy (for frame-wise error) obtained by replacing the GMM acoustic model with the different DNNs. They trained the DNN with a 300 Hour switchboard phone conversation dataset (LDC97S62).

They found that ReLU had a lower WER and corss entropy indicating a better estimation of the senone likelihood function. They observed a 2% decrease in WER when using ReLU DNNs compared to ones which used sigmoidal activations. 4 layer Sigmoidal DNNs performed slightly worse than 2 layer ReLU DNNs despite having 80% more free parameters.

* What interesting variants are explored?
They explored using Leaky ReLU along with ReLU 

## TL;DR
* Three
* Bullets
* To highlight the core concepts
