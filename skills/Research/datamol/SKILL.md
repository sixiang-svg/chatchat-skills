---
id: datamol
name: Datamol
description: Pythonic wrapper for RDKit simplified for drug discovery tasks like SMILES parsing, standardization, and conformer generation.
category: Research
requires: []
examples:
  - Standardize these SMILES strings using the Datamol library.
  - Generate 3D conformers for this molecule using Datamol.
---
# Datamol

Pythonic wrapper around RDKit with simplified interface and sensible defaults. Preferred for standard drug discovery: SMILES parsing, standardization, descriptors, fingerprints, clustering, 3D conformers, parallel processing. Returns native rdkit.Chem.Mol objects. For advanced control or custom parameters, use rdkit directly.

## Instruction
- Parse input SMILES strings or molecular files into native RDKit molecule objects using the simplified Datamol interface.
- Apply standardization protocols to handle salts, formal charges, and tautomers for consistent molecular representation.
- Utilize built-in functions for molecular featurization, including the calculation of descriptors and fingerprints.
- Execute 3D conformer generation using sensible defaults for drug discovery tasks.
- Implement parallel processing wrappers to efficiently manage large-scale molecular libraries.
- Transition to direct RDKit calls for advanced control if specific custom parameters are required.

## When to Use
- When standardizing large batches of SMILES strings for chemical databases.
- When preparing 3D molecular structures (conformers) for downstream virtual screening or docking.
- When performing rapid molecular clustering or analysis in early-stage drug discovery.

## Output
- Cleaned and standardized molecular data in SMILES or Mol object formats.
- A summary of generated 3D conformers, including energy minimization status.
- Performance logs for parallelized batch processing tasks.