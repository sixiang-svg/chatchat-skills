---
id: rdkit
name: RDKit
description: Pythonic wrapper for RDKit simplified for drug discovery: SMILES parsing, standardization, descriptors, 3D conformers, and parallel processing.
category: Research
requires: []
examples:
  - Standardize these SMILES strings using the RDKit library.
  - Generate 3D conformers for this molecule using RDKit in Python.
---

# RDKit

Pythonic wrapper around RDKit with simplified interface and sensible defaults. Preferred for standard drug discovery: SMILES parsing, standardization, descriptors, fingerprints, clustering, 3D conformers, parallel processing. Returns native rdkit.Chem.Mol objects. For advanced control or custom parameters, use rdkit directly.

## Instruction
- Parse chemical identifiers (SMILES, InChI) into native RDKit molecule objects for programmatic manipulation.
- Apply molecular standardization protocols to handle salts, formal charges, and tautomers for consistent data representation.
- Utilize featurization methods to generate molecular fingerprints (e.g., Morgan, ECFP) or calculate physicochemical descriptors.
- Execute substructure searching or similarity calculations to identify specific chemical scaffolds within a library.
- Conduct 3D structure generation and energy minimization for molecules to prepare them for docking analysis.
- Implement parallel processing for large-scale chemical databases to maximize computational efficiency.

## When to Use
- When performing molecular property prediction or standardizing chemical datasets for machine learning.
- When searching for structural analogs or calculating molecular similarity in drug discovery workflows.
- When preparing 3D molecular conformations for structure-based drug design.

## Output
- Cleaned and standardized chemical data formatted as SMILES or SDF files.
- Molecular property reports and feature matrices (fingerprints) for downstream analysis.
- Visualizations of chemical structures and conformer generation logs.