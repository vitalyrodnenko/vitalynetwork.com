---
title: "Weekly Digest, Week 14, 2026"
date: 2026-04-05
description: "Self-organizing AI agents outperform the hierarchical setups we design for them, and the research puts numbers on why that matters."
tags: ["weekly-digest", "ai", "agents", "llm"]
keywords: ["weekly digest", "AI agents", "LLM inference", "Claude Code", "Vitaly Rodnenko"]
---

What caught my attention in W14.

## How Anthropic built Claude Code

Someone reverse-engineered Claude Code from the npm source maps and wrote 18 chapters on it. The architecture is more interesting than you'd expect: an async generator drives the entire agent loop across four compression layers; sub-agents share prompt cache prefixes to cut costs by 95%; file-based memory uses a Sonnet side-query for recall instead of embeddings. The book is free to read and written for engineers building their own agentic systems, with "Apply This" sections at the end of every chapter. <a href="https://claude-code-from-source.com" rel="nofollow noindex">Source</a>

## LLM agents self-organize better than we design them

A paper out of arxiv tested 25,000 tasks across 8 models, 4 to 256 agents, and 8 coordination protocols ranging from rigid hierarchy to full self-organization. The result: a hybrid protocol that gives agents minimal structure and lets them self-assign roles outperforms centralized coordination by 14%. The system generated 5,006 unique roles from just 8 agents. Stronger models self-organize better; weaker ones still need structure. The practical conclusion is blunt: give agents a mission and a capable model, not a pre-assigned role. Open-source models reached 95% of closed-source quality at 24x lower cost. <a href="https://arxiv.org/abs/2603.28990" rel="nofollow noindex">Source</a>

## KVzap: Fast, Adaptive, and Faithful KV Cache Pruning

KV cache is one of the nastier constraints in long-context LLM inference. A vanilla 65B transformer with a 128k context needs around 335 GB of KV cache in bfloat16. It scales linearly with context length and becomes a wall fast. KVzap attacks this by using a small predictor model to identify which cached tokens are still useful for future generation, then pruning the rest while keeping a local window intact. On Qwen3 and Llama 3.1 models, it hits 2 to 4x compression with negligible accuracy loss. Code is on GitHub via NVIDIA. <a href="https://arxiv.org/abs/2601.07891" rel="nofollow noindex">Source</a>

## The Human Operating System

Phil Fugate (AWS) makes a case for cognitive friction as the mechanism of learning, not a side effect of it. The studies he cites are solid: Roediger and Karpicke found that students who actively retrieved material from memory forgot 13% over two days; students who restudied the same material forgot 56%. Sparrow et al. showed that when people know they can look something up, they're less likely to retain the information at all: the brain offloads before any conscious decision to do so. The aviation parallel is good: pilots who relied on autopilot from the start had worse manual recovery when automation failed. <a href="https://philfugate.dev/blog/the-human-operating-system/" rel="nofollow noindex">Source</a>

My position on this: I agree that building durable capability requires some period of doing it without the tool. But the right sequence depends on the person. For my daughter, the plan is "learn how" first, then accelerate with AI. The point is not to keep her away from the technology, but to make sure the cognitive foundation is there before AI starts doing the work for her.
