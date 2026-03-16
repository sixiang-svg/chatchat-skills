---
id: molfeat
name: Molfeat
description: Molecular featurization for ML including ECFP, MACCS, descriptors, and pretrained models like ChemBERTa.
category: Research
requires: []
examples:
  - Featurize this SMILES list using ECFP4 fingerprints for a QSAR model.
  - How do I use pretrained ChemBERTa embeddings for molecular property prediction?
---

# Molfeat - Molecular Featurization Hub

## Overview

Molfeat is a comprehensive Python library for molecular featurization that unifies 100+ pre-trained embeddings and hand-crafted featurizers. Convert chemical structures (SMILES strings or RDKit molecules) into numerical representations for machine learning tasks including QSAR modeling, virtual screening, similarity searching, and deep learning applications. Features fast parallel processing, scikit-learn compatible transformers, and built-in caching.

## When to Use This Skill

This skill should be used when working with:
- **Molecular machine learning**: Building QSAR/QSPR models, property prediction
- **Virtual screening**: Ranking compound libraries for biological activity
- **Similarity searching**: Finding structurally similar molecules
- **Chemical space analysis**: Clustering, visualization, dimensionality reduction
- **Deep learning**: Training neural networks on molecular data
- **Featurization pipelines**: Converting SMILES to ML-ready representations
- **Cheminformatics**: Any task requiring molecular feature extraction

## Installation

## Core Concepts

Molfeat organizes featurization into three hierarchical classes:

### 1. Calculators (`molfeat.calc`)

Callable objects that convert individual molecules into feature vectors. Accept RDKit `Chem.Mol` objects or SMILES strings.

**Use calculators for:**
- Single molecule featurization
- Custom processing loops
- Direct feature computation

### 2. Transformers (`molfeat.trans`)

Scikit-learn compatible transformers that wrap calculators for batch processing with parallelization.

**Use transformers for:**
- Batch featurization of molecular datasets
- Integration with scikit-learn pipelines
- Parallel processing (automatic CPU utilization)


### 3. Pretrained Transformers (`molfeat.trans.pretrained`)

Specialized transformers for deep learning models with batched inference and caching.

**Use pretrained transformers for:**
- State-of-the-art molecular embeddings
- Transfer learning from large chemical datasets
- Deep learning feature extraction

## Instruction
- Select the appropriate featurizer based on the machine learning task (e.g., descriptors for QSAR, embeddings for deep learning).
- Utilize the `MoleculeTransformer` to convert SMILES or RDKit molecules into numerical arrays with scikit-learn compatibility.
- Implement pre-trained models such as ChemBERTa or GinModels to leverage learned chemical representations.
- Configure error handling to manage invalid SMILES strings and maintain dataset integrity during large-scale featurization.
- Optimize performance by using parallelized calculators and caching results for repeated workflows.
- Integrate the generated features into standard ML pipelines for clustering, similarity search, or property prediction.

## Output
- High-fidelity numerical feature arrays (NumPy/Pandas) ready for model training.
- Summaries of selected featurization parameters and configuration state (YAML).
- Diagnostic reports on data transformation success and handled molecular errors.