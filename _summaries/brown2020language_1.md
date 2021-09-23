---
layout: summary
title: Language Models are Few-Shot Learners
paper: brown2020language
# Please fill out info below
author: jaywhang
score: 10
---

## Core Idea

Builds upon their previous work [cite], this paper introduces GPT-3, a 175B-parameter autoregressive language model.
The main discovery of this paper is the model's ability to perform few-shot learning **without gradient steps or fine-tuning**.
This paper presents an extremely thorough large-scale study of GPT-3's performance on a wide range of NLP tasks.
Their experiments also test GPT-3 on a few non-standard tasks that further push the limits of of the pre-trained language model.

## Technical Description

### Training Details

GPT-3 largely follows the architecture of GPT-2, with a minor difference of having alternating dense and sparse (locally-banded) attention.
In order to train such a large model, the authors also created a custom text corpus.
Specifically, they combined five different datasets with custom preprocessing to ensure the quality of examples.
The exact weight and size the number of tokens (after Byte-Pair Encoding) is shown in **Table 1**.

[Table 1: Include Table 2.2 from the paper]

Due to the size of their model, they determined the learning rate and batch size based on the level of gradient noise.
Lastly, to accomodate such a large model with extremely large batch size (~3.2M), they employed model parallelism across V100 GPUs.

### Evaluation Details

To test the model's few-shot learning capability, they sampled examples from the training data for each task and fed that as conditioning input, followed by 1-2 blank lines.

[TODO: Include more details about how each task is transformed to be compatible with GPT-3 interface?]

## Experimental Results

The majority of this paper consists of discussion and analysis of the experimental results.
For starters, GPT-3 somewhat expectedly achieves a significantly improved performance over previous SOTA model on zero-shot Penn Tree Bank language modeling.

Then the authors evaluate GPT-3 on several Q&A tasks.
One very interesting trend we observe is in **Figure 1**.
As shown in the plot, the performance of GPT-3 variants continue to improve **linearly** with respect to the parameter count without diminishing returns.
This shows that the language model continues to absorb knowledge as its capacity increases.

[Figure 1: Include Figure 3.3 from paper]

Another interesting result is on machine translation, where GPT-3 improves upon previous **supervised** methods in a few-shot setting for certain language pairs.
The authors point out that GPT-3, a model primarily trained on Engish (93% of the training corpus), achieves a large improvement of 5 BLEU score compared to previous unsupervised methods.
This further speaks for GPT-3's capability as an English language model.
**Table 3.4** shows GPT-3's machine translation performance relative to previous supervised and unsupervised approaches.

[Table 2: Include Table 3.4 from paper]

Lastly, the authors perform a few non-standard NLP experiments.
For example, they ask GPT-3 to solve simple two/three-digit arithmetic problems by feeding questions such as "Q: What is 34 minus 53?".
Surprisingly, as shown in **Figure 2**, the two largest models achieve a significant performance boost for these tasks.
Overall, the authors show that GPT-3 is able to perform two- and three-digit arithmetic problems somewhat reliably.

[Figure 2: Include Figure 3.10 from paper]

## Limitations and Societal Impacts

Thankfully, the authors also discuss the limitations got GPT-3, along with the broader impact such a large language model may have on the society.

They mention that the biggest weakness of GPT-3 is in its text synthesis ability.
Even though it essentially achieved SOTA results on most tasks, it still possesses the known issues of autoregressive language models.
Such issues include losing coherence over long passages, repetition in samples, self-contradictions, and generating non-sequitur text.
As a general-purpose conversation model, it still lacks common sense that most human speakers have, such as basic understanding of physics.

There are some algorithmic weaknesses too.
Because GPT-3 is an **autoregressive** model, it cannot be directly used to perform tasks that require filling in blanks, re-reading passages, and comparing two pieces of content.
As expected, the authors note that making a bi-directional analogue of GPT-3 is a promising direction to explore.

Lastly, the authors argue that GPT-3 still has extremely poor sample efficiency compared to humans.
The training data is way larger than the amount of text people typically see in their lifetime.
Yet, the model is still unable to come close to human performance for many NLP tasks (TODO: which ones specifically?).


[TODO: Add more discussion on Broader Impact]

## Conclusion & My Comments

[TODO: Maybe talk about Solomonoff Induction here and how it may justify the use of autoregressive modeling]

## TL;DR
* This paper introduced GPT-3, the largest Transformer-based language model produced at the time with 175 billion parameters.
* GPT-3 exhibits phenomenal few-zhot learning performance and outperforms previous models (even some supervised or fine-tuned ones) on a wide variety of NLP tasks.
* While the performance is impressive, GPT-3 still comes with many restrictions and very subpar learning capabilities compared to humans.
