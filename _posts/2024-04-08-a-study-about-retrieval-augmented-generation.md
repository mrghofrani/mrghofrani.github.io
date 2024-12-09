---
layout: single
title:  "A Study About Retrieval Augmented Generation"
date:   2024-04-08 00:00:00 +0330
author: Mohammadreza Ghofrani
classes: wide
---

"Why Was Sam Altman Fired As CEO of OpenAI?" this is one of the questions that ChatGPT fails to answer by default. Though ChatGPT is not wrong, it says, "I don't know":

> I'm sorry, but that statement is not accurate. As of my last knowledge update in January 2022, Sam Altman was the CEO of OpenAI ...

However, ChatGPT is not always good at saying "I don't know". Sometimes, it provides inaccurate answers for the questions. For instance, I have asked ChatGPT "When was the Habsburg Empire founded?". it said:

> The Habsburg Empire, also known as the Austro-Hungarian Empire, was founded in 1804 ...

Hence ChatGPT believes that the Habsburg Empire was founded in 1804. A simple inquiry from [Wikipedia](https://en.wikipedia.org/wiki/Habsburg_monarchy) reveals that the Habsburg Empire lasted for nearly six centuries and was founded in 1282. This time ChatGPT is *wrong*!

The problem where LLMs tend to think "they *know* everything *accurately*." and can answer every question asked is known as *hallucination* and results in providing the wrong or inaccurate information.

One of the solutions for the hallucination problem is to augment relevant documents
alongside the given prompt. The model uses the information provided in the documents
while generating a response, crafting a better and more precise response. This solution called Retrieval Augmented Generation.

As its name suggests, Retrieval Augmented Generation (RAG) consists of three components: Retriever, Augmenter, and Generator. Retriever fetches the most relevant information from the knowledge base, Augmenter concats the query with the given documents, and Generator crafts the response to the user’s query.

The studies in this field can be divided into two classes: fine-grained and End-to-End. Fine-grained studies tend to tackle just one of the components of the RAG architecture; However, End-to-End methods modify the architecture as a whole.

# Fine-grained

## Retrieval fine-graining

Most ideas in this part have come from the Information Retrieval (IR) field in the NLP. The main questions these researchers try to answer are "How to effectively represent a document as a vector?", "What is the best method to chunk the document?", or "How to effectively index the documents?".

One of the interesting ideas that can be classified in this category, is the idea proposed in the paper "GENERATE RATHER THAN RETRIEVE", where they have proposed to utilize an LLM to generate a document based on user query and then pass the generated document to the next phase where an LLM utilizes it to craft the response.

## Augmentation fine-graining

These studies focus on finding the optimum query and the best way to append the retrieved document to prepare an effective prompt. Some studies revealed LLMs tend to attend more to their first or last input tokens. Thus, some studies suggested reranking the top $k$ retrieved documents and positioning the most important one as the first (or last) augmented document. Others tend to extract the principle information out of the text not only to help LLM grasp crucial ideas, but also to face the context limitations. Some other studies try to curate the best prompt for each use case, proposing a *routing* functionality to choose the best prompt from available options.
## Generation fine-graining

The studies focusing on the generation module mostly inherit their ideas from the text generation field of the NLP. Before the introduction of LLMs, most researchers tried to fine-tune state-of-the-are models such as GPT and T5 that have good generation capability for the RAG. Recently, most studies utilize LLMs due to their good performance, ignoring the fine-tuning stage. However, there are still studies conducted that improve performance of the LLMs by fine-tuning on their target domain.
# End-to-End

Some research like RETRO tend to train the whole RAG architecture as a whole. The idea behind these examinations is better alignment of generative model with the retriever part. Other studies also try to provide feedback from generator to the retrieval to improve retrieved documents quality and ease the generator's task.

# Reference

Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., … Wang, H. (2024). Retrieval-Augmented Generation for Large Language Models: A Survey. arXiv [Cs.CL]. Retrieved from http://arxiv.org/abs/2312.10997