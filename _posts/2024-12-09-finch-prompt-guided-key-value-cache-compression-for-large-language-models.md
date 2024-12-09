---
layout: single
title:  "FINCH: Prompt-guided Key-Value Cache Compression for Large Language Models"
date:   2024-12-09 00:00:00 +0330
author: Mohammadreza Ghofrani
classes: wide
excerpt: "The paper introduces FINCH, a cache compression algorithm that avoids the need to train large language models (LLMs) from scratch."
---

## Summary

The paper introduces FINCH, a cache compression algorithm that avoids the need to train large language models (LLMs) from scratch. The main idea behind FINCH is to cache the most relevant entries from the key matrices in the attention layer of the transformer. These matrices are crucial because they store information about previous tokens, which the transformer uses for processing.

![FINCH Diagram](/assets/images/2024-12-09-finch-prompt-guided-key-value-cache-compression-for-large-language-models/diagram.png)


The figure above illustrates the overall procedure of FINCH. In the Prefill stage, the document is divided into chunks, which are then fed into the transformer. Let's break this process down step by step: first chunck is tokenized into 0 and 1 tokens (denoted by blue boxes with dotted lines) are fed into the transformer, along with the prompt tokens (denoted by a yellow box with a dotted line), and the attention matrices are calculated. Next, Second chunck is tokenized and fed into the transformer alongside the prompt. In this step, the most relevant chunks from the previous ones are fetched and added to the current attention matrices. This process continues until the transformer has consumed all the chunks.

Once the relative importance of each chunk in relation to the input prompt is determined, only the processed values are used during the generation step. Using this method LLMs could consume larger volumes of text without fine-tuning.

In summary, FINCH splits the text into chunks, generates a vector summary for each chunk, and uses these summaries during the generation process to improve efficiency.

## Strenghs

- It’s plug-and-play and doesn’t require adapting the weights of the pre-trained transformers.
- It enables current pre-trained transformers to process long chunks of text without the need to adapt their weights.
- Unlike the Key-Value cache mechanism, it requires less RAM to operate.

## Future Works

- Sharing cache across multiple user inputs, but the privacy concerns should be considered.
- The compression rate is equal among all layers. making it dynamic could be more usefull.

## References

Corallo, G., & Papotti, P. (11 2024). FINCH: Prompt-guided Key-Value Cache Compression for Large Language Models. Transactions of the Association for Computational Linguistics, 12, 1517–1532. doi:10.1162/tacl_a_00716