---
layout: single
title: "Instances Need More Care: Rewriting Prompts for Instances with LLMs in the Loop Yields Better Zero-Shot Performance"
date: 2024-11-06 00:00:00 +0330
author: Mohammadreza Ghofrani
classes: wide
excerpt: "This paper presents an approach where the task model generates an initial output, which is refined by a meta model to improve the input prompt, resulting in a more accurate final output."
---

## Summary

Unlike other approaches, which revise the output of the LLM to improve answer accuracy and prevent hallucinations, this paper focuses on the input prompt. It allows the language model (referred to as the task model) to generate an initial output. This output is then evaluated by another language model (the meta model) to refine the input prompt of the task model. Finally, the task model generates the final output based on the refined prompt.

## Strengths

Since the input prompts for LLMs are usually much shorter than their outputs, the method discussed in this paper—by focusing on crafting optimized input prompts—is significantly faster and more cost-effective.

## Weaknesses

Some limitations, such as hallucinations and vulnerabilities to role-playing prompts, are noted in the paper. In my opinion, these issues arise from the meta model being static compared to the task model. Therefore, an initial solution to mitigate these drawbacks could involve refining either the input prompt of the meta model or the output.

## My insights for future works

A general solution to improve the accuracy of LLMs is Retrieval-Augmented Generation (RAG). It would be interesting to explore whether incorporating RAG into task models or meta models would more effectively enhance performance within this structure.

## Reference

Srivastava, S., Huang, C., Fan, W., & Yao, Z. (2024, August). Instances Need More Care: Rewriting Prompts for Instances with LLMs in the Loop Yields Better Zero-Shot Performance. In L.-W. Ku, A. Martins, & V. Srikumar (Eds.), Findings of the Association for Computational Linguistics: ACL 2024 (pp. 6211–6232). doi:10.18653/v1/2024.findings-acl.371