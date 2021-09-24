---
layout: summary
title: 	Neural Machine Translation by Jointly Learning to Align and Translate
paper: {{bahdanau2014neural}}
# Please fill out info below
author: SShivang
score: 8/10
---

What is the core idea?

The core idea of the paper is doing neural machine translation using a encoder and decoder architecture. The primary model consists of an encoder, which takes in the input embeddings, as well as the embedding of the previous time step and outputs a hidden state. The decoder does the similar, where it takes the output embeddings (embedding of the translation), the previous time step and a context vector c. The context vector is a weighted sum of the hidden states of the encoder model.

How is it realized (technically)?

The paper introduces the concept of alignment. It learns a set of alignments that allow it to do better in translation.

How well does the paper perform?

The model reaches high BLEU scores. However, suffers as the sentences get larger.

What interesting variants are explored?

They explore different searches.


## TL;DR
* The core idea of the paper is doing neural machine translation using a encoder and decoder architecture.
* Introduce idea of attention
* Show improvement using BLEU score metric, however, does much worse on larger sentences.
