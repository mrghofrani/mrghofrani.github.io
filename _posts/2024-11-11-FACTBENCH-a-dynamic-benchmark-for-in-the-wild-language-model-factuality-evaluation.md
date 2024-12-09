---
layout: single
title: "FACTBENCH: A Dynamic Benchmark for in-the-wild Language Model Factuality Evaluation"
date: 2024-11-08 00:00:00 +0330
author: Mohammadreza Ghofrani
classes: wide
excerpt: "The paper presents two contributions: (a) FactBench, a benchmark for evaluating hallucination in LLMs, and (b) VERIFY, an evaluation framework designed to check for hallucinations in model responses."
---

## Summary

The paper presents two contributions: (a) FactBench, a benchmark for evaluating hallucination in LLMs, and (b) VERIFY, an evaluation framework designed to check for hallucinations in model responses.

![FactBench Diagram](/assets/images/2024-11-11-FACTBENCH-a-dynamic-benchmark-for-in-the-wild-language-model-factuality-evaluation/diagram.png)

Let’s start with VERIFY, as shown on the right in the figure above. After the LLM generates a response, VERIFY's Unit Extraction & Labeling component breaks it down into individual sentences. Then, the Unit Decontextualization component makes each sentence self-contained. Next, the Query Generation component crafts a Google Search query to fact-check each sentence. This component does not simply pass queries through; instead, it refines each query based on search results to find the most relevant information. Finally, the Final Judgment step classifies each sentence into supported, unsupported, or undecided categories. The following formula is used to score each response. In the formula, $$\lvert C \rvert$$ represents the number of unsupported sentences, $$\lvert U \rvert$$ represents undecided sentences, and $$\lvert V \rvert$$ is the total number of decomposed sentences. The $$\alpha$$ factor is used to diminish the impact of undecided sentences, as these sentences may be correct but lack sufficient evidence in search results for verification.

$$H(R) = \frac{\lvert C \rvert +\alpha \lvert U \rvert}{\sqrt{\lvert V \rvert}}$$

Now, let’s briefly describe how FactBench is built. To create a fact-checking benchmark that evaluates LLM responses based on real-world prompts, the authors used the LMSYS-Chat-1M dataset as the foundation for FactBench. After standard preprocessing, they applied the [BERTopic](https://github.com/MaartenGr/BERTopic) library to cluster and retain only niche user requests. Next, they used Llama-70B-Instruct to filter out unverifiable prompts. Usefulness scores were then used to classify prompts into hard, moderate, and easy categories. Finally, the prompts and their responses in LMSYS-Chat-1M were processed through the VERIFY framework to determine hallucination scores.

## Strengths

- FactBench could be updated in a regular basis.
- Because the VERIFY framework operates online, it can accurately check newly revealed facts.

## Weaknesses

- Since the VERIFY framework checks facts online, hallucination scores cannot be compared over time, because the facts may change. For example, the response to the question “*The latest 50 kernel versions and release times of Linux*” will change as new versions of the Linux kernel are introduced. Similarly, consider the prompt “*iPhone vs Samsung flagship phone, pros and cons, in a table format.*” A previously trained model might answer this question in different ways, and over time, its statements—although correct at the time—could become outdated. Therefore, In my opinion, an ideal hallucination evaluation framework should use the LLM’s own resources to assess the model's adherence to facts. This way, LLMs should not be penalized for things they were not exposed to during training.
- The benchmark only measures the LLMs hallucination in the first round of the conversation.
- They primarily used Llama 70B-Instruct for labeling their dataset; however, GPT-4 was also accessible, which was more powerful and, in my opinion, more cost-effective.

## Reference

Bayat, F. F., Zhang, L., Munir, S., & Wang, L. (2024). FactBench: A Dynamic Benchmark for In-the-Wild Language Model Factuality Evaluation. arXiv [Cs.CL]. Retrieved from http://arxiv.org/abs/2410.22257