---
id: evaluating-llms-harness
name: Evaluating LLMs Harness
description: Evaluate LLMs across academic benchmarks (MMLU, HumanEval, GSM8K) using standardized prompts and metrics.
category: Research
author: Orchestra Research
version: 1.0.0
requires: []
examples:
  - Run the MMLU benchmark on a local HuggingFace model.
  - Create a custom evaluation task for a domain-specific LLM.
---

# lm-evaluation-harness - LLM Benchmarking

## Instruction
- Choose the appropriate benchmark suite based on the model's target capability, such as MMLU for reasoning or HumanEval for code.
- Configure the model backend (e.g., HuggingFace, vLLM) and specify hardware parameters like device IDs and batch size.
- Execute the evaluation using standard settings, such as 5-shot prompts for MMLU to ensure comparability with published papers.
- Integrate with vLLM backends for 5-10x faster inference during large-scale evaluation tasks.
- Track training progress by running periodic evaluations on checkpoints and plotting learning curves across diverse tasks.
- Enable code execution for code-based benchmarks like HumanEval to ensure accurate score calculation.

## When to Use
- When benchmarking model quality across academic standards for model release or research papers.
- When tracking the performance of an LLM during different stages of training or fine-tuning.
- When comparing the relative performance of multiple local or remote models using standardized metrics.

## Output
- Standardized performance reports containing accuracy scores, standard errors, and sample predictions.
- Comparison tables and learning curves showing performance across multiple models or training steps.
- Detailed JSON results ready for integration into research documentation or leaderboards.
