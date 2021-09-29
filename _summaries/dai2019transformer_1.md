---
layout: summary
title: Summary
paper: dai2019transformer
# Please fill out info below
author: slycane9
score: 9
---

## Core Idea
The authors developed a new Transformer-XL model that had two features that separated itself from other "Vanilla" Transformers of the time in regards to creating Language Models.

## Implementation

First, Transformer-XL used Segment-Level Recurrence and State Reuse to avoid fixed length context segments.  This is done by storing the hidden state of a segment not just for the next segment, but also for future segments afterwards.  This gives the model a sense of extended "history" as segment dependencies reach farther into future segments.  Technically, this is realized with a recurrence mechanism that links two segments together and propgates their hidden states throughout the layer.

![norecurrence](dai2019transformer_1a.png)
![recurrence](dai2019transformer_1b.png)


Advantages of this change are two-fold.  
* First, having a model of longer-term dependancy avoids context fragmentation, a problem experienced by prior transformers on this task.  
* Second, the recursive nature of the model allows faster training as information in previous segments can be easily accessed in later segments.


The second feature of Transformer-XL, which is necesary to achieve the benefits of the first Segment-Level Recurrence feature, is the introduction of Relative Positional Encodings.  In order to facilitate the re-use of prior segments, temporal bias is defined relatively in this method, rather than statistically.  Relative positional encodings thus further facilitates the previously mentioned advantages of Segment-Level Recurrence.


## Performance

In terms of how Transformer-XL performs, results showed that it outperforms state-of-the-art models in both perplexity and bits per character.

![result1](dai2019transformer_1c.png)


Transformer-XL also took less time to evaluate than the state-of-the-art language models.

![result2](dai2019transformer_1d.png)


## TL;DR
* Prior language model Transformers suffer from fixed-length context and context fragmentation.
* Transformer-XL avoids this using Segment-Level Recurrence and Relative Positional Encodings for longer-term dependencies.
* Transformer-XL outperforms state-of-the-art in perplexity, bits per character, and validation time.
