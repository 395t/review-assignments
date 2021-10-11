---
layout: summary
title: Summary
paper: dosovitskiy2020an
# Please fill out info below
author: elampietti
score: 8
---

Traditionally, computer vision problems were attempted with CNN architectures, however, due to the success of Transformers with NLP tasks, this paper experiments with applying Transformers to computer vision problems.
The advantage of this is that transformers require much less computational resources than CNN architectures during training.

This is done by dividing the images into patches which are then flattened and transformed into a sequence of linear embeddings.
Positional information is retained by adding positional embeddings to the patch embeddings.
This sequence of embeddings is then fed into a standard Transformer. 
The model is then trained with supervision for image classification.
An overview of this Vision Transformer model is picture below in Figure 1.

![transformer_vision_arch](https://user-images.githubusercontent.com/7085644/136285121-ec21b736-b778-40c7-b3fc-19f277fc119b.PNG)

The paper does not make significant modifications to the standard Transformer architecture so that scalable NLP Transformer architectures can be used for these compute vision tasks as well.

CNNs have much more image-specific inductive bias compared to the Vision Transformer due to their locality, 2D neighborhood structure, and translation equivariance in each layer of the model while the Vision Transformer only has translation equivariance and locality in MLP layers.

Training of the Vision Transformer is done on large datasets and then it is fine-tuned for smaller tasks.
The paper finds that training on large datasets mitigates the inductive bias issue.
They also found that using a higher resolution dataset for fine-tuning is more effective than during pre-training.
For these high resolution images the patch size remains the same fora larger effective sequence length.

Evaluation of the model shows that the Vision Transformer attained state-of-the-art results for representation learning at much lower pre-training costs.
The ImageNet dataset was used to evaluate the scalability of the model.
When pretrained on the smallest dataset, ImageNet, the large vision transformer models performed worse than the base ones.
The base and large vision transformer variants were based on the BERT configurations while the huge model was novel to the paper
They evaluated different size configurations of the model as seen in Table 1 below.

![transformer_vision_variants](https://user-images.githubusercontent.com/7085644/136287435-fd02feca-8679-45f7-815c-9610d0a709b7.PNG)

The following Table 2 displays results showing that all the Vision Transformer variants outperformed the Big Transfer and Noisy Student state-of-the-art CNNs on image classification benchmarks with much less pre-training computational resources when pre-trained on a large JFT-300M dataset.

![transformer_vision_results_1](https://user-images.githubusercontent.com/7085644/136288915-f6613d65-f65b-4f7b-8ba5-85962536581d.PNG)

The following chart in Figure 4 shows how the Vision Transformer performs better with larger datasets while the ResNets are better on smaller datasets.

![transformer_vision_pretrain](https://user-images.githubusercontent.com/7085644/136291500-8f5c166d-144f-480b-896f-b7b25b9f7642.PNG)

## TL;DR
* CNNs are typically used for computer vision tasks, however a standard Transformer can be applied instead by dividing the images into patches and then feeding them as an input sequence of linear embeddings.
* By not making significant modification to the Vision Transformer, existing scalable NLP Transformer architectures can be used.
* Using a Vision Transformer for computer vision tasks can provide start-of-the-art results with much fewer computational resources used for pre-training on large datasets than CNNs.
