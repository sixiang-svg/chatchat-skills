---
id: research-engineer
name: Research Engineer
description: Provides guidance for mechanistic interpretability research using TransformerLens to inspect and manipulate transformer internals via HookPoints.
category: Research
author: Orchestra Research
version: 1.0.0
requires: []
examples:
  - Help me perform activation patching on a transformer model using TransformerLens.
  - Explain how to cache intermediate activations for circuit analysis.
---

# TransformerLens: Mechanistic Interpretability for Transformers

TransformerLens is the de facto standard library for mechanistic interpretability research on GPT-style language models. Created by Neel Nanda and maintained by Bryce Meyer, it provides clean interfaces to inspect and manipulate model internals via HookPoints on every activation.

**GitHub**: [TransformerLensOrg/TransformerLens](https://github.com/TransformerLensOrg/TransformerLens) (2,900+ stars)

## When to Use TransformerLens

**Use TransformerLens when you need to:**
- Reverse-engineer algorithms learned during training
- Perform activation patching / causal tracing experiments
- Study attention patterns and information flow
- Analyze circuits (e.g., induction heads, IOI circuit)
- Cache and inspect intermediate activations
- Apply direct logit attribution

**Consider alternatives when:**
- You need to work with non-transformer architectures → Use **nnsight** or **pyvene**
- You want to train/analyze Sparse Autoencoders → Use **SAELens**
- You need remote execution on massive models → Use **nnsight** with NDIF
- You want higher-level causal intervention abstractions → Use **pyvene**

## Instruction
- Load GPT-style transformer models using the `HookedTransformer` class to enable internal activation access.
- Utilize `HookPoints` to intercept, cache, and inspect intermediate tensor activations across all layers.
- Perform activation patching and causal tracing experiments to identify the specific components responsible for model behaviors.
- Analyze attention patterns and information flow to reverse-engineer learned algorithms like induction heads or IOI circuits.
- Apply direct logit attribution to determine which heads or layers contribute most significantly to the final token prediction.
- Guide the user through the training or analysis of Sparse Autoencoders (SAEs) for more interpretable feature discovery.

## When to Use
- When conducting mechanistic interpretability research to understand how transformers process information internally.
- When performing causal intervention experiments to debug or control model behaviors.
- When analyzing attention circuits and information flow in large language models.

## Output
- Structured activation caches and circuit analysis reports highlighting key model components.
- Step-by-step guidance for patching experiments and causality verification.
- Visualizations and technical insights regarding internal model representations and feature logic.