---
id: denario
name: Denario
description: Multiagent AI system automating the scientific research pipeline from hypothesis generation to publication-ready LaTeX manuscripts.
category: Research
requires: []
examples:
  - Generate a novel research hypothesis for this climate dataset using Denario.
  - Write a journal-formatted LaTeX manuscript based on my recent computational results.
---

# Denario

## Overview

Denario is a multiagent AI system designed to automate scientific research workflows from initial data analysis through publication-ready manuscripts. Built on AG2 and LangGraph frameworks, it orchestrates multiple specialized agents to handle hypothesis generation, methodology development, computational analysis, and paper writing.

## Instruction
- Initialize the research project by defining the data context and available computational tools.
- Orchestrate specialized agents to generate novel research hypotheses based on the data description.
- Develop a structured methodology that outlines the computational experiments needed to test the hypothesis.
- Execute the methodology to generate computational results, analysis, and visualizations.
- Synthesize all findings into a journal-formatted LaTeX manuscript using specific styles like `Journal.APS`.
- Ensure research reproducibility by maintaining structured outputs for every stage of the pipeline.

## When to Use This Skill

Use this skill when:
- Analyzing datasets to generate novel research hypotheses
- Developing structured research methodologies
- Executing computational experiments and generating visualizations
- Conducting literature searches for research context
- Writing journal-formatted LaTeX papers from research results
- Automating the complete research pipeline from data to publication

## Output
- A defined research hypothesis and a detailed methodology document.
- Computational findings and visualizations ready for scientific interpretation.
- A complete LaTeX source package and a formatted PDF of the final manuscript.

## LLM API Configuration

Denario requires API keys from supported LLM providers. Supported providers include:
- Google Vertex AI
- OpenAI
- Other LLM services compatible with AG2/LangGraph

Store API keys securely using environment variables or `.env` files. 
## Core Research Workflow

Denario follows a structured four-stage research pipeline.

### 1. Data Description

Define the research context by specifying available data and tools


### 2. Idea Generation

Generate research hypotheses from the data description.


This produces a research question or hypothesis based on the described data. Alternatively, provide a custom idea


### 3. Methodology Development

Develop the research methodology


This creates a structured approach for investigating the hypothesis. Can also accept markdown files with custom methodologies


### 4. Results Generation

Execute computational experiments and generate analysis


This runs the methodology, performs computations, creates visualizations, and produces findings. Can also provide pre-computed results


### 5. Paper Generation

Create a publication-ready LaTeX paper


The generated paper includes proper formatting for the specified journal, integrated figures, and complete LaTeX source.

## Advanced Features

- **Multiagent orchestration**: AG2 and LangGraph coordinate specialized agents for different research tasks
- **Reproducible research**: All stages produce structured outputs that can be version-controlled
- **Journal integration**: Automatic formatting for target publication venues
- **Flexible input**: Manual or automated at each pipeline stage
- **Docker deployment**: Containerized environment with LaTeX and all dependencies

## Troubleshooting

Common issues and solutions:
- **API key errors**: Ensure environment variables are set correctly 
- **LaTeX compilation**: Install TeX distribution or use Docker image with pre-installed LaTeX
- **Package conflicts**: Use virtual environments or Docker for isolation
- **Python version**: Requires Python 3.12 or higher
