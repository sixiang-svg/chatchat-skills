---
id: adaptyv
name: Adaptyv
description: Automated protein testing platform for sequence validation. Submit sequences and receive experimental results for stability and activity.
category: Research
requires: []
examples:
  - Submit a set of protein sequences to Adaptyv for thermal stability testing.
  - Check the status of my recent protein expression experiment.
---

# Adaptyv

Adaptyv is a cloud laboratory platform that provides automated protein testing and validation services. Submit protein sequences via API or web interface and receive experimental results in approximately 21 days.

## Instruction
- Set up authentication by securing the `ADAPTYV_API_KEY` in environment variables or configuration files.
- Select the appropriate experiment type, such as Binding assays, Expression testing, or Thermostability characterization.
- Optimize protein sequences prior to submission to reduce aggregation, hydrophobic exposure, and unpaired cysteines.
- Use tools like NetSolP or SolubleMPNN for solubility filtering and sequence redesign before laboratory testing.
- Submit batches of protein sequences via the API, specifying experiment types and optional webhooks for result notification.
- Monitor experiment status and retrieve final stability or activity data upon completion (typically ~21 days).

## When to Use
- When performing high-throughput, automated protein validation in an AI-driven protein design pipeline.
- When experimental stability or binding affinity data is required for a large library of designed sequences.
- When optimizing candidate protein sequences for better laboratory expression and activity.

## Output
- Successfully submitted experiment IDs and status tracking summaries.
- Experimental validation results, including binding curves, expression levels, and stability metrics.
- Recommended sequence optimization workflows and solubility predictions.

## Quick Start

### Authentication Setup

Adaptyv requires API authentication. Set up your credentials:

1. Contact support@adaptyvbio.com to request API access (platform is in alpha/beta)
2. Receive your API access token
3. Set environment variable:


## Available Experiment Types

Adaptyv supports multiple assay types:

- **Binding assays** - Test protein-target interactions using biolayer interferometry
- **Expression testing** - Measure protein expression levels
- **Thermostability** - Characterize protein thermal stability
- **Enzyme activity** - Assess enzymatic function


## Protein Sequence Optimization

Before submitting sequences, optimize them for better expression and stability:

**Common issues to address:**
- Unpaired cysteines that create unwanted disulfides
- Excessive hydrophobic regions causing aggregation
- Poor solubility predictions

**Recommended tools:**
- NetSolP / SoluProt - Initial solubility filtering
- SolubleMPNN - Sequence redesign for improved solubility
- ESM - Sequence likelihood scoring
- ipTM - Interface stability assessment
- pSAE - Hydrophobic exposure quantification

## Important Notes

- Platform is currently in alpha/beta phase with features subject to change
- Not all platform features are available via API yet
- Results typically delivered in ~21 days
- Contact support@adaptyvbio.com for access requests or questions
- Suitable for high-throughput AI-driven protein design workflows
