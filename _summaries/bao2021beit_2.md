---
layout: summary
title: Summary
paper: bao2021beit
# Please fill out info below
author: liyanc
score: 6
---

* What is the core idea?

The authors aim to create a self-supervised pretaining model for vision tasks like BERT does as a language model.
The goal is to train a versatile vision model with only images in a self-supervised manner and the pre-trained model can be easily and cheaply transfered to a broad spectrum of vision tasks via finetuning.

* How is it realized (technically)?

  - Encode image patches as vocabularies with auto-encoders.
  - Train a vision transformer backbone against the "filling masks" pretraining task.

![image](https://user-images.githubusercontent.com/25853995/136881297-84247e17-93aa-4ea2-ba55-866cfaac1f91.png)


### Image tokenization

The tokenizer splits each image into patches with size at $$(P, P)$$ and flatten the array as a vector to be linearly projected.
The raw feature from the flattened image patches are fed into a discrete variational autoencoder to learn a tokenizer.
The authors chose dVAE since its latent space is an integer lattice $$\mathcal{V}^{h \times w}$$ serving as a discrete codebook for the vocabulary.
To train the non-differentiable model operating on a discrete latent space, the authors adopt Gumbel-softmax relaxation following the prior works.

### Self-supervised training

The ViT backbone is the standard transformer with the linearly projected flatten image patches as the input.
Following the standard transformer setup, the authors also add positional embeddings.

The pretraining task is again the same as the standard BERT setup to predict quasi-randomly masked out patches from the remaining context.
There are about 40% of image patches quasi-randomly masked out and replaced with a single learnable embedding shared through all masks.
The authors use the learned image tokens from the previous step as the prediction target for the training task.
Specifically, they ask the backbone to predict a probability distribution over the discrete token space on each masked position and maximize the joint probability of observations on all masked positions (prediction targets) as a MLE task.
Practially, it's formulated as minimizing NLL.

The author also proposed a quasi-random masking scheme to mask a continuous block at a time instead of spreading masks all over the image.

### Downsream tasks

The authors proposed some guidelines to transfer their vision model to downstream tasks.
Generally, they would append task-specific layers to the final output features of the backbone.
The expectation is that the vision model has learned sufficient feature representations to facilitate downsream tasks without expensive training from scratch.

* How well does the paper perform?

The proposed BEiT is primarily pre-trained on the ImageNet-1K dataset and finetuned on downstream tasks for evaluation.

  - Image classification achieves SOTA ![image](https://user-images.githubusercontent.com/25853995/136879772-751b5823-7e06-40cd-9124-8e0eaabb9ff5.png)
  - Image classification after fine-tuning on larger resolutions, still SOTA ![image](https://user-images.githubusercontent.com/25853995/136880161-a998a0b9-277c-4646-8037-a88457c8d629.png)
  - Semantic segmentation, SOTA ![image](https://user-images.githubusercontent.com/25853995/136880251-36088978-d73a-4f6b-853c-9eae4351c39e.png)

* What interesting variants are explored?

The authors ablate various components of the proposed method and compare their image classification performance as follows, which shows that the choice of block quasi-random masking and pre-training target space has significant impact on the performance.
Futhermore, the authors conclude that the choice of discrete latent space as prediction targets facilitate the model to learn semantic information in addition to pixel regression.
![image](https://user-images.githubusercontent.com/25853995/136880452-3f005322-ba65-4036-9561-d27bf0ba7381.png)


## TL;DR
* Combine ViT and BERT to give powerful and versatile off-the-shelf vision model for a broad spectrum downstream tasks.
* Splits images into patches and encode them as discrete tokens via dVAE as pre-training task targets.
* Feed flattened image patches into the Transformer backbone to train the model against the patch tokens from the previous step.
