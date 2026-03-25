---
id: diffdock
name: Diffdock
description: Diffusion-based molecular docking to predict 3D protein-ligand binding poses and confidence scores for virtual screening.
category: Research
requires: []
examples:
  - Predict the binding pose for this ligand-protein complex using DiffDock.
  - How do I run a virtual screening campaign for this compound library?
---

# DiffDock: Molecular Docking with Diffusion Models

## Overview

DiffDock is a diffusion-based deep learning tool for molecular docking that predicts 3D binding poses of small molecule ligands to protein targets. It represents the state-of-the-art in computational docking, crucial for structure-based drug discovery and chemical biology.

**Core Capabilities:**
- Predict ligand binding poses with high accuracy using deep learning
- Support protein structures (PDB files) or sequences (via ESMFold)
- Process single complexes or batch virtual screening campaigns
- Generate confidence scores to assess prediction reliability
- Handle diverse ligand inputs (SMILES, SDF, MOL2)

**Key Distinction:** DiffDock predicts **binding poses** (3D structure) and **confidence** (prediction certainty), NOT binding affinity (ΔG, Kd). Always combine with scoring functions (GNINA, MM/GBSA) for affinity assessment.

## When to Use This Skill

This skill should be used when:

- "Dock this ligand to a protein" or "predict binding pose"
- "Run molecular docking" or "perform protein-ligand docking"
- "Virtual screening" or "screen compound library"
- "Where does this molecule bind?" or "predict binding site"
- Structure-based drug design or lead optimization tasks
- Tasks involving PDB files + SMILES strings or ligand structures
- Batch docking of multiple protein-ligand pairs

## Instruction
- Verify the environment and GPU availability to ensure efficient diffusion-based sampling.
- Process protein structures (PDB) and ligand inputs (SMILES/SDF), using ESMFold for sequence-based protein inputs if necessary.
- Execute the docking inference while adjusting sampling density and steps to balance accuracy and performance.
- Analyze and rank the generated confidence scores (High > 0, Moderate -1.5 to 0, Low < -1.5) to identify the most likely poses.
- Interpret the results by distinguishing between structural confidence and actual binding affinity.
- Suggest integration with rescoring tools like GNINA or MM/GBSA for more accurate affinity assessment.

## Output
- A ranked set of predicted binding poses in SDF format with associated confidence scores.
- A summary analysis of docking performance across the provided complexes.
- Recommended next steps for affinity scoring and structural validation of the top poses.
