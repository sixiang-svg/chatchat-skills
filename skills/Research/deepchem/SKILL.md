---
id: deepchem
name: Deepchem
description: Molecular machine learning toolkit for ADMET prediction, graph neural networks, and MoleculeNet benchmarks in drug discovery.
category: Research
requires: []
examples:
  - Predict the toxicity of this molecule using a DeepChem GNN model.
  - Featurize this list of SMILES strings for a property prediction task.
---

# Deepchem

Molecular machine learning toolkit. Property prediction (ADMET, toxicity), GNNs (GCN, MPNN), MoleculeNet benchmarks, pretrained models, featurization, for drug discovery ML.

## Instruction
- Identify the specific drug discovery task, such as toxicity estimation or ADMET property prediction.
- Select and apply the correct featurizer, such as `GraphConv` or `CircularFingerprint`, to prepare SMILES for modeling.
- Load relevant benchmarking datasets from MoleculeNet if required for model evaluation.
- Initialize and configure deep learning models, focusing on Graph Neural Networks (GNNs) like GCN or MPNN.
- Perform property predictions using either pre-trained models or custom-trained architectures.
- Evaluate model performance using standard scientific metrics like RMSE or ROC-AUC.

## When to Use
- When predicting the biological activity or safety profiles of candidate molecules.
- When benchmarking molecular machine learning models against established drug discovery datasets.
- When featurizing chemical structures for integration into machine learning workflows.

## Output
- Property predictions or toxicity scores for the input molecular set.
- Model performance summaries and benchmarking results.
- A structured overview of the featurization and modeling pipeline.